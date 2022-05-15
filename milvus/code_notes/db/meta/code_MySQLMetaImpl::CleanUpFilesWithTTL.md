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
```