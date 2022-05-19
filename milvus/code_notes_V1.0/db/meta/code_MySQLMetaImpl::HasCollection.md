#1.MySQLMetaImpl::HasCollection

```
MySQLMetaImpl::HasCollection
--if (is_root) {                                                                                             
      HasCollectionQuery << "SELECT id FROM " << META_TABLES << " WHERE table_id = " << mysqlpp::quote       
                         << collection_id << " AND state <> " << std::to_string(CollectionSchema::TO_DELETE) 
                         << " AND owner_table = " << mysqlpp::quote << ""                                    
                         << ";";                                                                             
--} else {                                                                                                   
      HasCollectionQuery << "SELECT id FROM " << META_TABLES << " WHERE table_id = " << mysqlpp::quote       
                         << collection_id << " AND state <> " << std::to_string(CollectionSchema::TO_DELETE) 
                         << ";";                                                                             
  }                                                                                                          
--has_or_not = (res.num_rows() > 0);
```