#1.class ExecutionEngineImpl

```cpp
class ExecutionEngineImpl : public ExecutionEngine {

 protected:
    knowhere::VecIndexPtr index_ = nullptr;
#ifdef MILVUS_GPU_VERSION
    knowhere::VecIndexPtr index_reserve_ = nullptr;  // reserve the cpu index before copying it to gpu
#endif
    std::string location_;
    int64_t dim_;
    EngineType index_type_;
    MetricType metric_type_;

    std::unordered_map<std::string, DataType> attr_types_;
    std::unordered_map<std::string, std::vector<uint8_t>> attr_data_;
    std::unordered_map<std::string, size_t> attr_size_;
    query::BinaryQueryPtr binary_query_;
    int64_t vector_count_;

    milvus::json index_params_;
    int64_t gpu_num_ = 0;

    bool gpu_cache_enable_ = false;
};


```