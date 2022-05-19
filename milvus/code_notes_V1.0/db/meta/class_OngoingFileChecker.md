#1.class OngoingFileChecker

```cpp
using File2RefCount = std::map<uint64_t, int64_t>;
using Table2FileRef = std::map<std::string, File2RefCount>;

class OngoingFileChecker {
     private:
        std::mutex mutex_;
        meta::Table2FileRef ongoing_files_;  // collection id mapping to (file id mapping to ongoing ref-count)
    };
```