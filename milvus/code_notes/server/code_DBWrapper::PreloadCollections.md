#1.DBWrapper::PreloadCollections

```
DBWrapper::PreloadCollections
--if (preload_collections == "*")
----// load all tables
----std::vector<engine::meta::CollectionSchema> table_schema_array;
----db_->AllCollections(table_schema_array);
------DBImpl::AllCollections
--------status = meta_ptr_->AllCollections(all_collections);
----------MySQLMetaImpl::AllCollections
-=----------statement << "SELECT id, table_id, dimension, engine_type, index_params, index_file_size, metric_type"
                      << " ,owner_table, partition_tag, version, flush_lsn"
                      << " FROM " << META_TABLES << " WHERE state <> " << std::to_string(CollectionSchema::TO_DELETE);
----for (auto& schema : table_schema_array) {
------auto status = db_->PreloadCollection(nullptr, schema.collection_id_, partition_tags);
                   
```