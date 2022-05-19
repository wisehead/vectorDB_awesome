#1.class Cache

```cpp
template <typename ItemObj>
class Cache {
 private:
    std::string header_;
    int64_t usage_;
    int64_t capacity_;
    double freemem_percent_;

    LRU<std::string, ItemObj> lru_;
    mutable std::mutex mutex_;
};

```