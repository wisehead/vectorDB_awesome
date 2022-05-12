#1.MySQLMetaImpl::CreateCollectionFile

```
MySQLMetaImpl::CreateCollectionFile
--CollectionSchema collection_schema;
--collection_schema.collection_id_ = file_schema.collection_id_;
--auto status = DescribeCollection(collection_schema);
--NextFileId(file_schema.file_id_);
----MySQLMetaImpl::NextFileId
------SafeIDGenerator& id_generator = SafeIDGenerator::GetInstance();
      ss << id_generator.GetNextIDNumber();
--file_schema.dimension_ = collection_schema.dimension_;
        file_schema.file_size_ = 0;
        file_schema.row_count_ = 0;
        file_schema.created_on_ = utils::GetMicroSecTimeStamp();
        file_schema.updated_time_ = file_schema.created_on_;
        file_schema.index_file_size_ = collection_schema.index_file_size_;
        file_schema.index_params_ = collection_schema.index_params_;
        file_schema.engine_type_ = collection_schema.engine_type_;
        file_schema.metric_type_ = collection_schema.metric_type_;
--std::string id = "NULL";  // auto-increment
        std::string collection_id = file_schema.collection_id_;
        std::string segment_id = file_schema.segment_id_;
        std::string engine_type = std::to_string(file_schema.engine_type_);
        std::string file_id = file_schema.file_id_;
        std::string file_type = std::to_string(file_schema.file_type_);
        std::string file_size = std::to_string(file_schema.file_size_);
        std::string row_count = std::to_string(file_schema.row_count_);
        std::string updated_time = std::to_string(file_schema.updated_time_);
        std::string created_on = std::to_string(file_schema.created_on_);
        std::string date = std::to_string(file_schema.date_);
        std::string flush_lsn = std::to_string(file_schema.flush_lsn_);
--mysqlpp::ScopedConnection connectionPtr(*mysql_connection_pool_, safe_grab_);
--mysqlpp::Query statement = connectionPtr->query();
--statement << "INSERT INTO " << META_TABLEFILES << " VALUES(" << id << ", " << mysqlpp::quote
                      << collection_id << ", " << mysqlpp::quote << segment_id << ", " << engine_type << ", "
                      << mysqlpp::quote << file_id << ", " << file_type << ", " << file_size << ", " << row_count
                      << ", " << updated_time << ", " << created_on << ", " << date << ", " << flush_lsn << ");";        
--mysqlpp::SimpleResult res = statement.execute()
--file_schema.id_ = res.insert_id();
--return utils::CreateCollectionFilePath(options_, file_schema);
----CreateCollectionFilePath
------table_file.location_ = parent_path + "/" + table_file.file_id_;
```