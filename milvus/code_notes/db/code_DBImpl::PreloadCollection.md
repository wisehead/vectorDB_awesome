#1.DBImpl::PreloadCollection

```
DBImpl::PreloadCollection
--if (partition_tags.empty()) 
----// no partition tag specified, means load whole collection
    // get files from root collection
----auto status = meta_ptr_->FilesToSearch(collection_id, files_holder);
------MySQLMetaImpl::FilesToSearch
--------statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, date,"
                      << " engine_type, created_on, updated_time"
                      << " FROM " << META_TABLEFILES << " WHERE table_id = " << mysqlpp::quote << collection_id;
--------statement << " AND"
                      << " (file_type = " << std::to_string(SegmentSchema::RAW)
                      << " OR file_type = " << std::to_string(SegmentSchema::TO_INDEX)
                      << " OR file_type = " << std::to_string(SegmentSchema::INDEX) << ");";
----status = meta_ptr_->ShowPartitions(collection_id, partition_array);
------MySQLMetaImpl::ShowPartitions
--------statement << "SELECT table_id, id, state, dimension, created_on, flag, index_file_size,"
                      << " engine_type, index_params, metric_type, partition_tag, version, flush_lsn FROM "
                      << META_TABLES << " WHERE owner_table = " << mysqlpp::quote << collection_id << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";                      
----for (auto& schema : partition_array) {
            partition_ids.insert(schema.collection_id_);
        }
--else
----status = GetPartitionsByTags(collection_id, partition_tags, partition_name_array);
------DBImpl::GetPartitionsByTags
----for (auto& partition_name : partition_name_array) {
            partition_ids.insert(partition_name);

--// get files from partitions
--status = meta_ptr_->FilesToSearchEx(collection_id, partition_ids, files_holder);       
----MySQLMetaImpl::FilesToSearchEx

--// step 2: load file one by one
--milvus::engine::meta::SegmentsSchema& files_array = files_holder.HoldFiles();

--for (auto& file : files_array)
----if (file.file_type_ == meta::SegmentSchema::FILE_TYPE::RAW ||
            file.file_type_ == meta::SegmentSchema::FILE_TYPE::TO_INDEX ||
            file.file_type_ == meta::SegmentSchema::FILE_TYPE::BACKUP) {
            engine_type =
                utils::IsBinaryMetricType(file.metric_type_) ? EngineType::FAISS_BIN_IDMAP : EngineType::FAISS_IDMAP;
----else {
            engine_type = (EngineType)file.engine_type_;
        }
--ExecutionEnginePtr engine =EngineFactory::Build(file.dimension_, file.location_, engine_type, (MetricType)file.metric_type_, json);
--status = engine->Load(true);
```