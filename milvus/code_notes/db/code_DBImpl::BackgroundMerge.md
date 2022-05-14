#1.DBImpl::BackgroundMerge

```cpp
DBImpl::BackgroundMerge
--for (auto& collection_id : collection_ids)
----auto old_strategy = merge_mgr_ptr_->Strategy();
----if (force_merge_all) {
            merge_mgr_ptr_->UseStrategy(MergeStrategyType::ADAPTIVE);
----}
----auto status = merge_mgr_ptr_->MergeFiles(collection_id);
------MergeManagerImpl::MergeFiles
```