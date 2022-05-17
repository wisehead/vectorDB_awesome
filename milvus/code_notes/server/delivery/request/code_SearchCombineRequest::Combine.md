#1.SearchCombineRequest::Combine

```
SearchCombineRequest::Combine
--if (request_list_.empty()) 
----// validate first request input
----auto status = ValidationUtil::ValidateCollectionName(request->CollectionName());
----status = ValidationUtil::ValidateSearchTopk(request->TopK());
----// assign base parameters                                   
----collection_name_ = request->CollectionName();               
----min_topk_ = request->TopK() - MAX_TOPK_GAP / 2;             
----if (min_topk_ < 0) {                                        
------min_topk_ = 0;                                          
----}                                                           
----max_topk_ = request->TopK() + MAX_TOPK_GAP / 2;             
----if (max_topk_ > QUERY_MAX_TOPK) {                           
------max_topk_ = QUERY_MAX_TOPK;                             
----}                                                           
----extra_params_ = request->ExtraParams();                                                                         
----GetUniqueList(request->PartitionList(), partition_list_);   
----GetUniqueList(request->FileIDList(), file_id_list_);        
--request_list_.push_back(request);
--vectors_data_.vector_count_ += request->VectorsData().vector_count_;
```