#1.class WebServer

```cpp
class WebServer {
 public:
    static WebServer&
    GetInstance() {
        static WebServer web_server;
        return web_server;
    }

    void
    Start();

    void
    Stop();

 private:
    WebServer() {
        try_stop_.store(false);
    }

    ~WebServer() = default;

    Status
    StartService();
    Status
    StopService();

 private:
    std::atomic_bool try_stop_;

    std::shared_ptr<std::thread> thread_ptr_;
};
```