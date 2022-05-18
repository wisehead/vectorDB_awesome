#1.DBImpl::CreateCollection

```
DBImpl::CreateCollection
--if (options_.wal_enable_) {
----temp_schema.flush_lsn_ = wal_mgr_->CreateCollection(collection_schema.collection_id_);
------WalManager::CreateCollection
--return meta_ptr_->CreateCollection(temp_schema);
```