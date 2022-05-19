#1.class SpanInterceptorFactory

```cpp
class SpanInterceptorFactory : public ::grpc::experimental::ServerInterceptorFactoryInterface {
 public:
    explicit SpanInterceptorFactory(GrpcInterceptorHookHandler* hook_handler) : hook_handler_(hook_handler) {
    }

    ::grpc::experimental::Interceptor*
    CreateServerInterceptor(::grpc::experimental::ServerRpcInfo* info) override;

 private:
    GrpcInterceptorHookHandler* hook_handler_;
};
```