#1.class SearchCombineRequest

```cpp

class SearchCombineRequest : public BaseRequest {

 private:
    std::string collection_name_;
    engine::VectorsData vectors_data_;
    int64_t min_topk_ = 0;
    int64_t search_topk_ = 0;
    int64_t max_topk_ = 0;
    milvus::json extra_params_;
    std::set<std::string> partition_list_;
    std::set<std::string> file_id_list_;

    std::vector<SearchRequestPtr> request_list_;

    int64_t combine_max_nq_ = COMBINE_MAX_NQ;
};
```