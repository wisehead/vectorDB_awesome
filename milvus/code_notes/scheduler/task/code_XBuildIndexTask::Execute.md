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
```