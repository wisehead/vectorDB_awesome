#1.class MemTableFile

```cpp
class MemTableFile : public server::CacheConfigHandler {
 private:
    const std::string collection_id_;
    meta::SegmentSchema table_file_schema_;
    meta::MetaPtr meta_;
    DBOptions options_;
    size_t current_mem_;

    //    ExecutionEnginePtr execution_engine_;
    segment::SegmentWriterPtr segment_writer_ptr_;
};  // MemTableFile
```