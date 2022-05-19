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
--for (auto group : id_groups) 
----statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, date,"
                          << " engine_type, created_on, updated_time"
                          << " FROM " << META_TABLEFILES << " WHERE table_id in (";
                for (size_t i = 0; i < group.size(); i++) {
                    statement << mysqlpp::quote << group[i];
                    if (i != group.size() - 1) {
                        statement << ",";
                    }
                }
                statement << ")";

                // End
                statement << " AND"
                          << " (file_type = " << std::to_string(SegmentSchema::RAW)
                          << " OR file_type = " << std::to_string(SegmentSchema::TO_INDEX)
                          << " OR file_type = " << std::to_string(SegmentSchema::INDEX) << ");";

                LOG_ENGINE_DEBUG_ << "FilesToSearch: " << statement.str();                          
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