#1.MergeManagerImpl::MergeFiles

```
MergeManagerImpl::MergeFiles
--status = meta_ptr_->FilesToMerge(collection_id, files_holder);
----MySQLMetaImpl::FilesToMerge
------statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, 		date, engine_type, created_on, updated_time" << " FROM " << META_TABLEFILES << " WHERE 		table_id = " << mysqlpp::quote << collection_id << " AND file_type = " << 		std::to_string(SegmentSchema::RAW) << " ORDER BY row_count DESC;";
--status = strategy_->RegroupFiles(files_holder, files_groups);
----MergeSimpleStrategy::RegroupFiles
--for (auto& group : files_groups) {
----MergeTask task(meta_ptr_, options_, group);
----status = task.Execute();
----files_holder.UnmarkFiles(group);
------FilesHolder::UnmarkFiles
--------for (auto& file : files) {
----------UnmarkFileInternal(file);

```