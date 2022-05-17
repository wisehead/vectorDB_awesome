#1.class SpanInterceptor

```cpp
class SpanInterceptor : public ::grpc::experimental::Interceptor {
 public:
    SpanInterceptor(::grpc::experimental::ServerRpcInfo* info, GrpcInterceptorHookHandler* hook_handler);

    void
    Intercept(::grpc::experimental::InterceptorBatchMethods* methods) override;

 private:
    ::grpc::experimental::ServerRpcInfo* info_;
    GrpcInterceptorHookHandler* hook_handler_;
    //    std::shared_ptr<opentracing::Tracer> tracer_;
    //    std::unique_ptr<opentracing::Span> span_;
};
```