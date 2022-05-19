#1. class Server

```cpp
namespace milvus {
namespace server {

class Server {
 private:
    int64_t daemonized_ = 0;
    int pid_fd_ = -1;
    std::string pid_filename_;
    std::string config_filename_;
};  // Server

}  // namespace server
}  // namespace milvus
```