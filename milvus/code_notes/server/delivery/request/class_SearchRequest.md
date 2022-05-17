#1.class SearchRequest

```cpp
class SearchRequest : public BaseRequest {
 private:
    const std::string collection_name_;
    const engine::VectorsData vectors_data_;
    int64_t topk_;
    milvus::json extra_params_;
    const std::vector<std::string> partition_list_;
    const std::vector<std::string> file_id_list_;

    TopKQueryResult& result_;

    // for validation
    milvus::engine::meta::CollectionSchema collection_schema_;
};
```