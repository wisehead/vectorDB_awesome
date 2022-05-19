#1.XBuildIndexTask::Load

```
XBuildIndexTask::Load
--if (auto job = job_.lock())
----auto build_index_job = std::static_pointer_cast<scheduler::BuildIndexJob>(job);
----auto options = build_index_job->options();
----if (type == LoadType::DISK2CPU) 
------stat = to_index_engine_->Load(options.insert_cache_immediately_);
--file_size = to_index_engine_->Size();
----ExecutionEngineImpl::Size
------index_->Size
--------VecIndex::Size
----------return BlacklistSize() + UidsSize() + IndexSize();
--to_index_id_ = file_->id_;
--to_index_type_ = file_->file_type_;
```