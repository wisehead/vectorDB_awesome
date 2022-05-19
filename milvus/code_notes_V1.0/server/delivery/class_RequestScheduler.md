#1.class RequestScheduler

```cpp
class RequestScheduler {

 private:
    mutable std::mutex queue_mtx_;

    std::map<std::string, RequestQueuePtr> request_groups_;

    std::vector<ThreadPtr> execute_threads_;

    bool stopped_;
};
```