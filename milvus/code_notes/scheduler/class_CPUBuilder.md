#1.class CPUBuilder

```
class CPUBuilder {
 public:
    CPUBuilder() = default;

    void
    Start();

    void
    Stop();

    void
    Put(const TaskPtr& task);

 private:
    void
    worker_function();

 private:
    bool running_ = false;
    std::mutex mutex_;
    std::thread thread_;

    std::queue<TaskPtr> queue_;
    std::condition_variable queue_cv_;
    std::mutex queue_mutex_;
};
```