#1.DBImpl::Query

```
DBImpl::Query
--if (partition_tags.empty())
----// no partition tag specified, means search in whole collection
    // get files from root collection
----status = meta_ptr_->FilesToSearch(collection_id, files_holder);
------MySQLMetaImpl::FilesToSearch//母表
--------statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, date,"
                      << " engine_type, created_on, updated_time"
                      << " FROM " << META_TABLEFILES << " WHERE table_id = " << mysqlpp::quote << collection_id;

            // End
            statement << " AND"
                      << " (file_type = " << std::to_string(SegmentSchema::RAW)
                      << " OR file_type = " << std::to_string(SegmentSchema::TO_INDEX)
                      << " OR file_type = " << std::to_string(SegmentSchema::INDEX) << ");";
----// get files from partitions
        std::set<std::string> partition_ids;
        std::vector<meta::CollectionSchema> partition_array;
        status = meta_ptr_->ShowPartitions(collection_id, partition_array);
        for (auto& id : partition_array) {
            partition_ids.insert(id.collection_id_);
        }                      
----status = meta_ptr_->FilesToSearchEx(collection_id, partition_ids, files_holder);//子表
--else
----std::set<std::string> partition_name_array;
----status = GetPartitionsByTags(collection_id, partition_tags, partition_name_array);
----std::set<std::string> partition_ids;
        for (auto& partition_name : partition_name_array) {
            partition_ids.insert(partition_name);
        }
----status = meta_ptr_->FilesToSearchEx(collection_id, partition_ids, files_holder);
--status = QueryAsync(tracer.Context(), files_holder, k, extra_params, vectors, result_ids, result_distances);
```