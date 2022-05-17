#1.DBImpl::PreloadCollection

```
DBImpl::PreloadCollection
--if (partition_tags.empty()) 
----// no partition tag specified, means load whole collection
    // get files from root collection
----auto status = meta_ptr_->FilesToSearch(collection_id, files_holder);
------MySQLMetaImpl::FilesToSearch
--------statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, date,"
                      << " engine_type, created_on, updated_time"
                      << " FROM " << META_TABLEFILES << " WHERE table_id = " << mysqlpp::quote << collection_id;
--------statement << " AND"
                      << " (file_type = " << std::to_string(SegmentSchema::RAW)
                      << " OR file_type = " << std::to_string(SegmentSchema::TO_INDEX)
                      << " OR file_type = " << std::to_string(SegmentSchema::INDEX) << ");";
----status = meta_ptr_->ShowPartitions(collection_id, partition_array);
------MySQLMetaImpl::ShowPartitions
--------statement << "SELECT table_id, id, state, dimension, created_on, flag, index_file_size,"
                      << " engine_type, index_params, metric_type, partition_tag, version, flush_lsn FROM "
                      << META_TABLES << " WHERE owner_table = " << mysqlpp::quote << collection_id << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";                      
----for (auto& schema : partition_array) {
            partition_ids.insert(schema.collection_id_);
        }
--else
----
```