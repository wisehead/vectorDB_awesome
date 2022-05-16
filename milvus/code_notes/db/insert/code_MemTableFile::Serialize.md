#1.MemTableFile::Serialize

```
MemTableFile::Serialize
--auto status = segment_writer_ptr_->Serialize();
----SegmentWriter::Serialize
--table_file_schema_.file_size_ = segment_writer_ptr_->Size();
--table_file_schema_.row_count_ = segment_writer_ptr_->VectorCount();
--// if index type isn't IDMAP, set file type to TO_INDEX if file size exceed index_file_size
  // else set file type to RAW, no need to build index
--if (table_file_schema_.engine_type_ != (int)EngineType::FAISS_IDMAP &&
        table_file_schema_.engine_type_ != (int)EngineType::FAISS_BIN_IDMAP) {
        table_file_schema_.file_type_ =
            (size >= table_file_schema_.index_file_size_) ? meta::SegmentSchema::TO_INDEX : meta::SegmentSchema::RAW;
--} else {
        table_file_schema_.file_type_ = meta::SegmentSchema::RAW;
--}
--if (options_.insert_cache_immediately_) {
----segment_writer_ptr_->Cache();
```