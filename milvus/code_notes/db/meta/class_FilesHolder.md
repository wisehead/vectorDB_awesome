#1.class FilesHolder

```cpp
class FilesHolder {
 private:
    std::mutex mutex_;
    milvus::engine::meta::SegmentsSchema hold_files_;
    std::set<uint64_t> unique_ids_;
};

```