#1.MergeTask::Execute

```
MergeTask::Execute
--// step 1: create collection file
--meta::SegmentSchema collection_file;
--collection_file.collection_id_ = collection_id;
--collection_file.file_type_ = meta::SegmentSchema::NEW_MERGE;
--Status status = meta_ptr_->CreateCollectionFile(collection_file);
----MySQLMetaImpl::CreateCollectionFile
------statement << "INSERT INTO " << META_TABLEFILES << " VALUES(" << id << ", " << 		mysqlpp::quote<< collection_id << ", " << mysqlpp::quote << segment_id << ", " << 		engine_type << ", "<< mysqlpp::quote << file_id << ", " << file_type << ", " << file_size 		<<", " << row_count<< ", " << updated_time << ", " << created_on << ", " << date << ", " 		<< flush_lsn << ");";
// step 2: merge files
--utils::GetParentPath(collection_file.location_, new_segment_dir);
--auto segment_writer_ptr = std::make_shared<segment::SegmentWriter>(new_segment_dir);
```