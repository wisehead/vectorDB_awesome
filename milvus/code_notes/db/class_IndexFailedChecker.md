#1.class IndexFailedChecker

```cpp
class IndexFailedChecker {

 private:
    std::mutex mutex_;
    Table2FileErr index_failed_files_;  // collection id mapping to (file id mapping to failed times)
};
```