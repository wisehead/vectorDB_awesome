#1.class BuildMgr

```cpp
class BuildMgr {
 public:
    explicit BuildMgr(int64_t concurrent_limit) : available_(concurrent_limit) {
    }

 public:
    void
    Put() {
        std::lock_guard<std::mutex> lock(mutex_);
        ++available_;
    }

    bool
    Take() {
        std::lock_guard<std::mutex> lock(mutex_);
        if (available_ < 1) {
            return false;
        } else {
            --available_;
            return true;
        }
    }

    int64_t
    NumOfAvailable() {
        return available_;
    }

 private:
    std::int64_t available_;
    std::mutex mutex_;
};
```