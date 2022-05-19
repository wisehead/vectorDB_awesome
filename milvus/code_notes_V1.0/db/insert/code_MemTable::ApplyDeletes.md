#1.MemTable::ApplyDeletes

```
MemTable::ApplyDeletes
--auto status = meta_->FilesByType(collection_id_, file_types, files_holder);
----MySQLMetaImpl::FilesByType
--milvus::engine::meta::SegmentsSchema files = files_holder.HoldFiles();
--// which file need to be apply delete
--std::unordered_map<size_t, std::vector<segment::doc_id_t>> ids_to_check_map;  // file id mapping to delete ids
--for (auto& file : files)
----utils::GetParentPath(file.location_, segment_dir);
    segment::SegmentReader segment_reader(segment_dir);
    segment::IdBloomFilterPtr id_bloom_filter_ptr;
    segment_reader.LoadBloomFilter(id_bloom_filter_ptr);
----for (auto& id : doc_ids_to_delete_) {
------if (id_bloom_filter_ptr->Check(id)) {
--------ids_to_check_map[file.id_].emplace_back(id);
----}
--// release unused files
--for (auto& file : files) {
        if (ids_to_check_map.find(file.id_) == ids_to_check_map.end()) {
            files_holder.UnmarkFile(file);
        }
    }
--milvus::engine::meta::SegmentsSchema hold_files = files_holder.HoldFiles();
--for (auto& file : hold_files)
----status = meta_->GetCollectionFilesBySegmentId(segment_id, segment_holder);
------MySQLMetaImpl::GetCollectionFilesBySegmentId
--------statement << "SELECT id, table_id, segment_id, engine_type, file_id, file_type, file_size, "
                      << "row_count, date, created_on"
                      << " FROM " << META_TABLEFILES << " WHERE segment_id = " << mysqlpp::quote << segment_id
                      << " AND file_type <> " << std::to_string(SegmentSchema::TO_DELETE) << ";";
--------for (auto& resRow : res) {
----------files_holder.MarkFile(file_schema);
----// Get all index that contains blacklist in cache
----milvus::engine::meta::SegmentsSchema& segment_files = segment_holder.HoldFiles();
----for (auto& segment_file : segment_files) 
------auto data_obj_ptr = cache::CpuCacheMgr::GetInstance()->GetIndex(segment_file.location_);
------auto index = std::static_pointer_cast<knowhere::VecIndex>(data_obj_ptr);
------if (index != nullptr) {
--------faiss::ConcurrentBitsetPtr blacklist = index->GetBlacklist();
--------if (blacklist == nullptr) {
----------// to update and set the blacklist
----------blacklist = std::make_shared<faiss::ConcurrentBitset>(index->Count());
----------indexes.emplace_back(index);
----------blacklists.emplace_back(blacklist);
--------} else {
----------// just to update the blacklist
----------indexes.emplace_back(nullptr);
----------blacklists.emplace_back(blacklist);
--------}
----status = segment_reader.LoadUids(uids);
----status = segment_reader.LoadBloomFilter(id_bloom_filter_ptr);
----auto& ids_to_check = ids_to_check_map[file.id_];
----segment::DeletedDocsPtr deleted_docs = std::make_shared<segment::DeletedDocs>();
----std::sort(ids_to_check.begin(), ids_to_check.end());
----for (size_t i = 0; i < uids.size(); ++i)
------auto found = std::binary_search(ids_to_check.begin(), ids_to_check.end(), uids[i]);
------if (found)
--------deleted_docs->AddDeletedDoc(i);
--------id_bloom_filter_ptr->Remove(uids[i]);
--------for (auto& blacklist : blacklists) {
----------blacklist->set(i);
----for (size_t i = 0; i < indexes.size(); ++i) {
            if (indexes[i]) {
                indexes[i]->SetBlacklist(blacklists[i]);
            }
        }
----status = segment_writer.WriteDeletedDocs(deleted_docs);
----status = segment_writer.WriteBloomFilter(id_bloom_filter_ptr);
----// Update collection file row count
----for (auto& segment_file : segment_files) {
            if (segment_file.file_type_ == meta::SegmentSchema::RAW ||
                segment_file.file_type_ == meta::SegmentSchema::TO_INDEX ||
                segment_file.file_type_ == meta::SegmentSchema::INDEX ||
                segment_file.file_type_ == meta::SegmentSchema::BACKUP) {
                segment_file.row_count_ -= deleted_docs->GetSize();
                files_to_update.emplace_back(segment_file);
            }
----}        
--status = meta_->UpdateCollectionFilesRowCount(files_to_update);
----SqliteMetaImpl::UpdateCollectionFilesRowCount
------std::string statement = "UPDATE " + std::string(META_TABLEFILES) + " SET row_count = " + row_count
                                    + " , updated_time = " + updated_time + " WHERE file_id = " + file.file_id_ + ";";
```