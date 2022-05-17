#1.class BlockingQueue

```cpp
template <typename T>
class BlockingQueue {
 public:
    BlockingQueue() : mtx(), full_(), empty_() {
    }

    virtual ~BlockingQueue() {
    }

    BlockingQueue(const BlockingQueue& rhs) = delete;

    BlockingQueue&
    operator=(const BlockingQueue& rhs) = delete;

    void
    Put(const T& task);

    T
    Take();

    T
    Front();

    T
    Back();

    size_t
    Size();

    bool
    Empty();

    void
    SetCapacity(const size_t capacity);

 protected:
    mutable std::mutex mtx;
    std::condition_variable full_;
    std::condition_variable empty_;
    std::queue<T> queue_;
    size_t capacity_ = 32;
};
```
