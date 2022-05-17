#1.DBImpl::BackgroundBuildIndex

```
DBImpl::BackgroundBuildIndex
--meta_ptr_->FilesToIndex(files_holder);
----MySQLMetaImpl::FilesToIndex
------statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, date,"
                      << " engine_type, created_on, updated_time"
                      << " FROM " << META_TABLEFILES << " WHERE file_type = " << std::to_string(SegmentSchema::TO_INDEX)
                      << ";";
--milvus::engine::meta::SegmentsSchema to_index_files = files_holder.HoldFiles();
--Status status = index_failed_checker_.IgnoreFailedIndexFiles(to_index_files);                      
```