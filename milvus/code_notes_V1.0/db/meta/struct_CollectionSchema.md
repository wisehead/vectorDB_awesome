#1.struct CollectionSchema

```
struct CollectionSchema {
    typedef enum {
        NORMAL,
        TO_DELETE,
    } TABLE_STATE;

    size_t id_ = 0;
    std::string collection_id_;
    int32_t state_ = (int)NORMAL;
    uint16_t dimension_ = 0;
    int64_t created_on_ = 0;
    int64_t flag_ = 0;
    int64_t index_file_size_ = DEFAULT_INDEX_FILE_SIZE;
    int32_t engine_type_ = DEFAULT_ENGINE_TYPE;
    std::string index_params_ = "{}";
    int32_t metric_type_ = DEFAULT_METRIC_TYPE;
    std::string owner_collection_;
    std::string partition_tag_;
    std::string version_ = CURRENT_VERSION;
    uint64_t flush_lsn_ = 0;
};  // CollectionSchema
```