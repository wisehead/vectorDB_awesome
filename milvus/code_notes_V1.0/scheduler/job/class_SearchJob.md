#1.class SearchJob

```cpp
class SearchJob : public Job {

 private:
    const std::shared_ptr<server::Context> context_;

    uint64_t topk_ = 0;
    milvus::json extra_params_;
    // TODO: smart pointer
    const engine::VectorsData& vectors_;

    Id2IndexMap index_files_;
    // TODO: column-base better ?
    ResultIds result_ids_;
    ResultDistances result_distances_;
    Status status_;

    query::GeneralQueryPtr general_query_;
    std::unordered_map<std::string, engine::meta::hybrid::DataType> attr_type_;
    uint64_t vector_count_;

    std::mutex mutex_;
    std::condition_variable cv_;
};

```