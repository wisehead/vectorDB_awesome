#1.class GrpcServer

```cpp
class GrpcServer {
 private:
    std::unique_ptr<::grpc::Server> server_ptr_;
    std::shared_ptr<std::thread> thread_ptr_;
};

```