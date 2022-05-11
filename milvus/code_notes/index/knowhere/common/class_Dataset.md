#1.class Dataset

```cpp
class Dataset {
 public:
    Dataset() = default;

    template <typename T>
    void
    Set(const std::string& k, T&& v) {
        std::lock_guard<std::mutex> lk(mutex_);
        data_[k] = std::make_shared<Value>(std::forward<T>(v));
    }

    template <typename T>
    T
    Get(const std::string& k) {
        std::lock_guard<std::mutex> lk(mutex_);
        try {
            return std::any_cast<T>(*(data_.at(k)));
        } catch (...) {
            throw std::logic_error("Can't find this key");
        }
    }

    const std::map<std::string, ValuePtr>&
    data() const {
        return data_;
    }

 private:
    std::mutex mutex_;
    std::map<std::string, ValuePtr> data_;
};
```