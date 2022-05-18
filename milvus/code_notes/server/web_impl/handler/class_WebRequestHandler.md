#1.class WebRequestHandler

```cpp
class WebRequestHandler {
 private:
    std::shared_ptr<Context> context_ptr_;
    RequestHandler request_handler_;
    std::unordered_map<std::string, engine::meta::hybrid::DataType> field_type_;
};

```