#1.SearchRequest::OnExecute

```
SearchRequest::OnExecute
--// step 4: check collection existence
--// only process root collection, ignore partition collection
--collection_schema_.collection_id_ = collection_name_;
--auto status = DBWrapper::DB()->DescribeCollection(collection_schema_);

--// step 5: check search parameters
--status = ValidationUtil::ValidateSearchParams(extra_params_, collection_schema_, topk_);
----ValidationUtil::ValidateSearchParams

--// step 6: check vector data according to metric type
--status = ValidationUtil::ValidateVectorData(vectors_data_, collection_schema_);

--// step 7: search vectors
--if (file_id_list_.empty()) 
----status = DBWrapper::DB()->Query(context_, collection_name_, partition_list_, (size_t)topk_, extra_params_,vectors_data_, result_ids, result_distances);
----DBImpl::Query
--else 
----status = DBWrapper::DB()->QueryByFileID(context_, file_id_list_, (size_t)topk_, extra_params_,vectors_data_, result_ids, result_distances);

--// step 8: construct result array
        milvus::server::ContextChild tracer(context_, "Constructing result");
        result_.row_num_ = vectors_data_.vector_count_;
        result_.id_list_.swap(result_ids);
        result_.distance_list_.swap(result_distances);
```