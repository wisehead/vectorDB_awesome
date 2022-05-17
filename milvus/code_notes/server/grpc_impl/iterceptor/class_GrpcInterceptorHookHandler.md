#1.class GrpcInterceptorHookHandler

```cpp
class GrpcInterceptorHookHandler {
 public:
    virtual void
    OnPostRecvInitialMetaData(::grpc::experimental::ServerRpcInfo* server_rpc_info,
                              ::grpc::experimental::InterceptorBatchMethods* interceptor_batch_methods);

    virtual void
    OnPreSendMessage(::grpc::experimental::ServerRpcInfo* server_rpc_info,
                     ::grpc::experimental::InterceptorBatchMethods* interceptor_batch_methods);
};
```