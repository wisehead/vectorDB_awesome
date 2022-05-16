#1.MySQLMetaImpl::ShowPartitions

```
MySQLMetaImpl::ShowPartitions
--statement << "SELECT table_id, id, state, dimension, created_on, flag, index_file_size,"
                      << " engine_type, index_params, metric_type, partition_tag, version, flush_lsn FROM "
                      << META_TABLES << " WHERE owner_table = " << mysqlpp::quote << collection_id << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";
--
```