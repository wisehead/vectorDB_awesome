#1.class CreateCollectionRequest

```cpp
class CreateCollectionRequest : public BaseRequest {
 public:
    static BaseRequestPtr
    Create(const std::shared_ptr<milvus::server::Context>& context, const std::string& collection_name,
           int64_t dimension, int64_t index_file_size, int64_t metric_type);

 protected:
    CreateCollectionRequest(const std::shared_ptr<milvus::server::Context>& context, const std::string& collection_name,
                            int64_t dimension, int64_t index_file_size, int64_t metric_type);

    Status
    OnExecute() override;

 private:
    const std::string collection_name_;
    int64_t dimension_;
    int64_t index_file_size_;
    int64_t metric_type_;
};
```