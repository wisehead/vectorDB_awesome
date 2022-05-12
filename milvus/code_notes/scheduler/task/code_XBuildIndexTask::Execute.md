#1.XBuildIndexTask::Execute

```
XBuildIndexTask::Execute
--job = job_.lock()//weak_ptr -> shared_ptr
--auto build_index_job = std::static_pointer_cast<scheduler::BuildIndexJob>(job);

--// step 1: create collection file
  engine::meta::SegmentSchema table_file;
  table_file.collection_id_ = file_->collection_id_;
  table_file.segment_id_ = file_->file_id_;
  table_file.date_ = file_->date_;
  table_file.file_type_ = engine::meta::SegmentSchema::NEW_INDEX;
--engine::meta::MetaPtr meta_ptr = build_index_job->meta();
--Status status = meta_ptr->CreateCollectionFile(table_file);
----MemTableFile::CreateCollectionFile//or MySQL,SQLite interface

--// step 2: build index
--index = to_index_engine_->BuildIndex(table_file.location_, (EngineType)table_file.engine_type_);
----ExecutionEngineImpl::BuildIndex

--// step 3: if collection has been deleted, dont save index file
--MySQLMetaImpl::HasCollection

--// step 4: save index file
--index->Serialize();
----ExecutionEngineImpl::Serialize

--// step 5: update meta
--table_file.file_type_ = engine::meta::SegmentSchema::INDEX;
--table_file.file_size_ = server::CommonUtil::GetFileSize(table_file.location_);
--table_file.row_count_ = file_->row_count_;  // index->Count();
--auto origin_file = *file_;
--origin_file.file_type_ = engine::meta::SegmentSchema::BACKUP;

--engine::meta::SegmentsSchema update_files = {table_file, origin_file};
-- // makesure index file is sucessfully serialized to disk
--status = meta_ptr->UpdateCollectionFiles(update_files);
----MySQLMetaImpl::UpdateCollectionFiles
--build_index_job->BuildIndexDone(to_index_id_);
----BuildIndexJob::BuildIndexDone
------to_index_files_.erase(to_index_id);
------cv_.notify_all();
```