#1.class ThreadPool

```cpp
class ThreadPool {
 public:
    explicit ThreadPool(size_t threads, size_t queue_size = 1000);

    template <class F, class... Args>
    auto
    enqueue(F&& f, Args&&... args) -> std::future<typename std::result_of<F(Args...)>::type>;

    ~ThreadPool();

 private:
    // need to keep track of threads so we can join them
    std::vector<std::thread> workers_;

    // the task queue
    std::queue<std::function<void()> > tasks_;

    size_t max_queue_size_;

    // synchronization
    std::mutex queue_mutex_;

    std::condition_variable condition_;

    bool stop;
};
```