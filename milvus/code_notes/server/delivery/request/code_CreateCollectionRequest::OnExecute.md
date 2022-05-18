#1.CreateCollectionRequest::OnExecute

```
CreateCollectionRequest::OnExecute
--// step 1: check arguments
--auto status = ValidationUtil::ValidateCollectionName(collection_name_);
--status = ValidationUtil::ValidateTableDimension(dimension_, metric_type_);
--status = ValidationUtil::ValidateCollectionIndexFileSize(index_file_size_);
--status = ValidationUtil::ValidateCollectionIndexMetricType(metric_type_);
--// step 2: construct collection schema
        engine::meta::CollectionSchema collection_info;
        collection_info.collection_id_ = collection_name_;
        collection_info.dimension_ = static_cast<uint16_t>(dimension_);
        collection_info.index_file_size_ = index_file_size_;
        collection_info.metric_type_ = metric_type_;
--// some metric type only support binary vector, adapt the index type
        if (engine::utils::IsBinaryMetricType(metric_type_)) {
            if (collection_info.engine_type_ == static_cast<int32_t>(engine::EngineType::FAISS_IDMAP)) {
                collection_info.engine_type_ = static_cast<int32_t>(engine::EngineType::FAISS_BIN_IDMAP);
            } else if (collection_info.engine_type_ == static_cast<int32_t>(engine::EngineType::FAISS_IVFFLAT)) {
                collection_info.engine_type_ = static_cast<int32_t>(engine::EngineType::FAISS_BIN_IVFFLAT);
            }
        }
--// step 3: create collection
--status = DBWrapper::DB()->CreateCollection(collection_info);      
----DBImpl::CreateCollection  
```