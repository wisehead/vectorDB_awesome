#1.struct SegmentSchema

```cpp
struct SegmentSchema {
    typedef enum {
        NEW,
        RAW,
        TO_INDEX,
        INDEX,
        TO_DELETE,
        NEW_MERGE,
        NEW_INDEX,
        BACKUP,
    } FILE_TYPE;

    size_t id_ = 0;
    std::string collection_id_;
    std::string segment_id_;
    std::string file_id_;
    int32_t file_type_ = NEW;
    size_t file_size_ = 0;
    size_t row_count_ = 0;
    DateT date_ = EmptyDate;
    uint16_t dimension_ = 0;
    // TODO(zhiru)
    std::string location_;
    int64_t updated_time_ = 0;
    int64_t created_on_ = 0;
    int64_t index_file_size_ = DEFAULT_INDEX_FILE_SIZE;  // not persist to meta
    int32_t engine_type_ = DEFAULT_ENGINE_TYPE;
    std::string index_params_;                   // not persist to meta
    int32_t metric_type_ = DEFAULT_METRIC_TYPE;  // not persist to meta
    uint64_t flush_lsn_ = 0;
};  // SegmentSchema
```