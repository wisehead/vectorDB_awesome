#1.DBImpl::StartMergeTask

```
DBImpl::StartMergeTask
--if (!merge_thread_results_.empty())
----if (merge_thread_results_.back().wait_for(span) == std::future_status::ready) {
------merge_thread_results_.pop_back();
--if (merge_thread_results_.empty()) 
----merge_thread_results_.push_back(merge_thread_pool_.enqueue(&DBImpl::BackgroundMerge, this, merge_collection_ids, force_merge_all));
------DBImpl::BackgroundMerge
```