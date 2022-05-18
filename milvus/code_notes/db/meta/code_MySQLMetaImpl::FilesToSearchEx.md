#1.MySQLMetaImpl::FilesToSearchEx

```
MySQLMetaImpl::FilesToSearchEx
--// get root collection information
--CollectionSchema collection_schema;
--collection_schema.collection_id_ = root_collection;
--auto status = DescribeCollection(collection_schema);
----MySQLMetaImpl::DescribeCollection
------statement << "SELECT id, state, dimension, created_on, flag, index_file_size, engine_type, index_params"
                      << " , metric_type ,owner_table, partition_tag, version, flush_lsn"
                      << " FROM " << META_TABLES << " WHERE table_id = " << mysqlpp::quote
                      << collection_schema.collection_id_ << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";
--// distribute id array to batches
--std::vector<std::vector<std::string>> id_groups;
--DistributeBatch(partition_id_array, id_groups);
```

#2.DistributeBatch

```
DistributeBatch
--
```