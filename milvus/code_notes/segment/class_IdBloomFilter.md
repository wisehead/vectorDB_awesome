#1.class IdBloomFilter

```cpp
class IdBloomFilter {
 private:
    scaling_bloom_t* bloom_filter_;
    //    const std::string name_ = "bloom_filter";
    std::mutex mutex_;
};
```