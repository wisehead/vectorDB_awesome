#1.class XSearchTask

```cpp
class XSearchTask : public Task {

 public:
    const std::shared_ptr<server::Context> context_;

    SegmentSchemaPtr file_;

    size_t index_id_ = 0;
    int index_type_ = 0;
    ExecutionEnginePtr index_engine_ = nullptr;

    // distance -- value 0 means two vectors equal, ascending reduce, L2/HAMMING/JACCARD/TONIMOTO ...
    // similarity -- infinity value means two vectors equal, descending reduce, IP
    bool ascending_reduce = true;
};
```