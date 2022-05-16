#1.DBImpl::ExecWalRecord

```
DBImpl::ExecWalRecord
--lambda collections_flushed

```

#2.lambda collections_flushed

```
lambda collections_flushed
--for (auto& collection : target_collection_names)
----meta_ptr_->GetCollectionFlushLSN(collection, lsn);
------statement << "SELECT flush_lsn FROM " << META_TABLES << " WHERE table_id = " << mysqlpp::quote << collection_id << ";";
--wal_mgr_->CollectionFlushed(collection_id, lsn);
----auto it_col = collections_.find(collection_id);
----if (it_col != collections_.end())
------for (auto& part : it_col->second) {
--------part.second.flush_lsn = lsn;
--std::set<std::string> merge_collection_ids;
--for (auto& collection : target_collection_names) {
----merge_collection_ids.insert(collection);
--StartMergeTask(merge_collection_ids);
--return max_lsn;
```