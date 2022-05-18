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

```cpp
std::vector<std::string> temp_group;
    //    constexpr uint64_t SQL_BATCH_SIZE = 50; // duplicate variable
    for (auto& id : id_array) {
        temp_group.push_back(id);
        if (temp_group.size() >= SQL_BATCH_SIZE) {
            id_groups.emplace_back(temp_group);
            temp_group.clear();
        }
    }

    if (!temp_group.empty()) {
        id_groups.emplace_back(temp_group);
    }
```