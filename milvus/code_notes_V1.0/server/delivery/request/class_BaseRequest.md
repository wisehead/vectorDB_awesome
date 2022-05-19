#1.class BaseRequest

```cpp
class BaseRequest {

 protected:
    const std::shared_ptr<milvus::server::Context> context_;

    RequestType type_;
    std::string request_group_;
    bool async_;
    Status status_;

 private:
    mutable std::mutex finish_mtx_;
    std::condition_variable finish_cond_;
    bool done_;

 public:
    const std::shared_ptr<milvus::server::Context>&
    Context() const {
        return context_;
    }
};
```