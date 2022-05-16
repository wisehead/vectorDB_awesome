#1.DBImpl::Start

```cpp
DBImpl::Start
--if (initialized_.load(std::memory_order_acquire)) 
----return Status::OK();
--initialized_.store(true, std::memory_order_release);
--// server may be closed unexpected, these un-merge files need to be merged when server restart
  // and soft-delete files need to be deleted when server restart
--std::set<std::string> merge_collection_ids;
--std::vector<meta::CollectionSchema> collection_schema_array;
--meta_ptr_->AllCollections(collection_schema_array);
----MySQLMetaImpl::AllCollections
--for (auto& schema : collection_schema_array) {
        merge_collection_ids.insert(schema.collection_id_);
    }
--StartMergeTask(merge_collection_ids, true);
----DBImpl::StartMergeTask
--// wal
--if (options_.wal_enable_)
----error_code = wal_mgr_->Init(meta_ptr_);
------WalManager::Init
----// recovery
----while (1) {
------auto error_code = wal_mgr_->GetNextRecovery(record);
------if (record.type == wal::MXLogType::None) {
--------break;
------ExecWalRecord(record);
```

#2.
