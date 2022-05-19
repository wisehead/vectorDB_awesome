#1.DBImpl::GetPartitionByTag

```
DBImpl::GetPartitionByTag
--// trim side-blank of tag, only compare valid characters
  // for example: " ab cd " is treated as "ab cd"
--std::string valid_tag = partition_tag;
--server::StringHelpFunctions::TrimStringBlank(valid_tag);
--if (valid_tag == milvus::engine::DEFAULT_PARTITON_TAG) 
----partition_name = collection_id;
----return
--status = meta_ptr_->GetPartitionName(collection_id, partition_tag, partition_name);
----MySQLMetaImpl::GetPartitionName
------statement << "SELECT table_id FROM " << META_TABLES << " WHERE owner_table = " << mysqlpp::quote
                      << collection_id << " AND partition_tag = " << mysqlpp::quote << valid_tag << " AND state <> "
                      << std::to_string(CollectionSchema::TO_DELETE) << ";";
```