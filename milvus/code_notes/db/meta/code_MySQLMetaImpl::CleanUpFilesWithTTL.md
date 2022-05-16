#1.MySQLMetaImpl::CleanUpFilesWithTTL

```
MySQLMetaImpl::CleanUpFilesWithTTL
--statement << "SELECT id, table_id, segment_id, engine_type, file_id, file_type, date"<< " FROM 		" << META_TABLEFILES << " WHERE file_type IN ("<< std::to_string(SegmentSchema::TO_DELETE) 		<< "," << std::to_string(SegmentSchema::BACKUP)<< ")"<< " AND updated_time < " << 		std::to_string(now - seconds * US_PS) << ";";
--SegmentSchema collection_file;
--std::vector<std::string> delete_ids;
--for (auto& resRow : res)
----FilesHolder::CanBeDeleted(collection_file)
------FilesHolder::CanBeDeleted
--------OngoingFileChecker::GetInstance().CanBeDeleted(file);
----------FilesHolder::OngoingFileChecker::CanBeDeleted
------------auto iter = ongoing_files_.find(schema.collection_id_);
------------if (iter == ongoing_files_.end()) 
--------------return true;
------------else
--------------auto it_file = iter->second.find(schema.id_);
--------------if (it_file == iter->second.end())
----------------return true;
--------------else
----------------return (it_file->second > 0) ? false : true;
----// erase file data from cache
    // because GetCollectionFilePath won't able to generate file path after the file is deleted
----utils::GetCollectionFilePath(options_, collection_file);
------std::string parent_path = ConstructParentFolder(options.path_, table_file);
--------std::string table_path = db_path + TABLES_FOLDER + table_file.collection_id_;
--------std::string partition_path = table_path + "/" + table_file.segment_id_;
------table_file.location_ = parent_path + "/" + table_file.file_id_;
----server::CommonUtil::EraseFromCache(collection_file.location_);
------CommonUtil::EraseFromCache
----if (collection_file.file_type_ == (int)SegmentSchema::TO_DELETE) 
------// delete file from disk storage
------utils::DeleteCollectionFilePath(options_, collection_file);
--------utils::GetCollectionFilePath(options, table_file);
--------boost::filesystem::remove(table_file.location_);
------delete_ids.emplace_back(std::to_string(collection_file.id_));
------collection_ids.insert(collection_file.collection_id_);
------segment_ids.insert(std::make_pair(collection_file.segment_id_, collection_file));
--// delete file from meta
--if (!delete_ids.empty())
----std::stringstream idsToDeleteSS;
----for (auto& id : delete_ids) {
------idsToDeleteSS << "id = " << id << " OR ";
----statement << "DELETE FROM " << META_TABLEFILES << " WHERE " << idsToDeleteStr << ";";
----statement.exec()
--// remove to_delete collections
--statement << "SELECT id, table_id"<< " FROM " << META_TABLES << " WHERE state = " << 		std::to_string(CollectionSchema::TO_DELETE)<< ";";
--mysqlpp::StoreQueryResult res = statement.store();
--for (auto& resRow : res) {
----size_t id = resRow["id"];
----std::string collection_id;
----resRow["table_id"].to_string(collection_id);
----utils::DeleteCollectionPath(options_, collection_id, false);  // only delete empty folder
----++remove_collections;
----idsToDeleteSS << "id = " << std::to_string(id) << " OR ";
--statement << "DELETE FROM " << META_TABLES << " WHERE " << idsToDeleteStr << ";";
--statement.exec()
--for (auto& collection_id : collection_ids)
----statement << "SELECT file_id"<< " FROM " << META_TABLEFILES << " WHERE table_id = " << mysqlpp::quote << collection_id << ";";
----mysqlpp::StoreQueryResult res = statement.store();
----if (res.empty()) {
------utils::DeleteCollectionPath(options_, collection_id);
--------std::vector<std::string> paths = options.slave_paths_;
--------paths.push_back(options.path_);
--------for (auto& path : paths)
----------std::string table_path = path + TABLES_FOLDER + collection_id;
----------boost::filesystem::remove_all(table_path);

```