#1.DBImpl::CreateCollection

```
DBImpl::CreateCollection
--if (options_.wal_enable_) {
----temp_schema.flush_lsn_ = wal_mgr_->CreateCollection(collection_schema.collection_id_);//DDL no WAL log record
------WalManager::CreateCollection
--return meta_ptr_->CreateCollection(temp_schema);
----MySQLMetaImpl::CreateCollection
------statement << "INSERT INTO " << META_TABLES << " VALUES(" << id << ", " << mysqlpp::quote << collection_id
                      << ", " << state << ", " << dimension << ", " << created_on << ", " << flag << ", "
                      << index_file_size << ", " << engine_type << ", " << mysqlpp::quote << index_params << ", "
                      << metric_type << ", " << mysqlpp::quote << owner_collection << ", " << mysqlpp::quote
                      << partition_tag << ", " << mysqlpp::quote << version << ", " << flush_lsn << ");";
```