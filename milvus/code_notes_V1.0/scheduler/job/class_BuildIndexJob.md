#1.class BuildIndexJob

```cpp
class BuildIndexJob : public Job, public server::CacheConfigHandler {
 private:
    Id2ToIndexMap to_index_files_;
    engine::meta::MetaPtr meta_ptr_;
    engine::DBOptions options_;

    Status status_;
    std::mutex mutex_;
    std::condition_variable cv_;
};
```