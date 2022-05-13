#1.class Context 

```cpp
class Context {
 private:
    std::string request_id_;
    BaseRequest::RequestType request_type_;
    std::shared_ptr<tracing::TraceContext> trace_context_;
    ConnectionContextPtr context_;
};

```