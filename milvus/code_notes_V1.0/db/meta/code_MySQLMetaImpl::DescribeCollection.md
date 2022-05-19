#1.MySQLMetaImpl::DescribeCollection

```
MySQLMetaImpl::DescribeCollection
--server::MetricCollector metric;
--mysqlpp::StoreQueryResult res;
--mysqlpp::ScopedConnection connectionPtr(*mysql_connection_pool_, safe_grab_);
--mysqlpp::Query statement = connectionPtr->query();
--statement << "SELECT id, state, dimension, created_on, flag, index_file_size, engine_type, index_params"
                      << " , metric_type ,owner_table, partition_tag, version, flush_lsn"
                      << " FROM " << META_TABLES << " WHERE table_id = " << mysqlpp::quote
                      << collection_schema.collection_id_ << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";
--res = statement.store();
--if (res.num_rows() == 1) {
            const mysqlpp::Row& resRow = res[0];
            collection_schema.id_ = resRow["id"];  // implicit conversion
            collection_schema.state_ = resRow["state"];
            collection_schema.dimension_ = resRow["dimension"];
            collection_schema.created_on_ = resRow["created_on"];
            collection_schema.flag_ = resRow["flag"];
            collection_schema.index_file_size_ = resRow["index_file_size"];
            collection_schema.engine_type_ = resRow["engine_type"];
            resRow["index_params"].to_string(collection_schema.index_params_);
            collection_schema.metric_type_ = resRow["metric_type"];
            resRow["owner_table"].to_string(collection_schema.owner_collection_);
            resRow["partition_tag"].to_string(collection_schema.partition_tag_);
            resRow["version"].to_string(collection_schema.version_);
            collection_schema.flush_lsn_ = resRow["flush_lsn"];
        }                       
```