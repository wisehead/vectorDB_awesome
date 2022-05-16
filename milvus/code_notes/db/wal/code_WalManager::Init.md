#1.WalManager::Init

```
WalManager::Init
--p_meta_handler_ = std::make_shared<MXLogMetaHandler>(mxlog_config_.mxlog_path);
--p_meta_handler_->GetMXLogInternalMeta(applied_lsn);
----MXLogMetaHandler::GetMXLogInternalMeta
--meta->GetGlobalLastLSN(recovery_start);
--MySQLMetaImpl::GetGlobalLastLSN
----statement << "SELECT global_lsn FROM " << META_ENVIRONMENT << ";";
--auto status = meta->AllCollections(collention_schema_array);
--for (auto& col_schema : collention_schema_array) {
----auto& collection = collections_[col_schema.collection_id_];
----auto& default_part = collection[""];
----default_part.flush_lsn = col_schema.flush_lsn_;
----update_limit_lsn(default_part.flush_lsn);

----std::vector<meta::CollectionSchema> partition_schema_array;
----status = meta->ShowPartitions(col_schema.collection_id_, partition_schema_array);
------MySQLMetaImpl::ShowPartitions
--------statement << "SELECT table_id, id, state, dimension, created_on, flag, index_file_size,"
                      << " engine_type, index_params, metric_type, partition_tag, version, flush_lsn FROM "
                      << META_TABLES << " WHERE owner_table = " << mysqlpp::quote << collection_id << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";
----for (auto& par_schema : partition_schema_array) {
------auto& partition = collection[par_schema.partition_tag_];
------partition.flush_lsn = par_schema.flush_lsn_;
------update_limit_lsn(partition.flush_lsn);
--if (applied_lsn < max_flushed_lsn) {
----// a new WAL folder?
----applied_lsn = max_flushed_lsn;
--if (recovery_start < min_flushed_lsn) {
----// not flush all yet
----recovery_start = min_flushed_lsn;
--for (auto& col : collections_) {
----for (auto& part : col.second) {
------part.second.wal_lsn = applied_lsn;

```