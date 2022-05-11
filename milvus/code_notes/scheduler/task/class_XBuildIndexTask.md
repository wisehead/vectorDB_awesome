#1.class XBuildIndexTask

```cpp
class XBuildIndexTask : public Task {
 public:
    explicit XBuildIndexTask(SegmentSchemaPtr file, TaskLabelPtr label);

    void
    Load(LoadType type, uint8_t device_id) override;

    void
    Execute() override;

 public:
    SegmentSchemaPtr file_;
    SegmentSchema table_file_;
    size_t to_index_id_ = 0;
    int to_index_type_ = 0;
    ExecutionEnginePtr to_index_engine_ = nullptr;
};

```