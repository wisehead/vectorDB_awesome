#1.class MergeTask

```cpp
class MergeTask {
 public:
    MergeTask(const meta::MetaPtr& meta, const DBOptions& options, meta::SegmentsSchema& files);

    Status
    Execute();

 private:
    meta::MetaPtr meta_ptr_;
    DBOptions options_;

    meta::SegmentsSchema files_;
};  // MergeTask
```