#1.ExecutionEngineImpl::Serialize

```
ExecutionEngineImpl::Serialize
--utils::GetParentPath(location_, segment_dir);
--auto segment_writer_ptr = std::make_shared<segment::SegmentWriter>(segment_dir);
--segment_writer_ptr->SetVectorIndex(index_);
----SegmentWriter::SetVectorIndex
------segment_ptr_->vector_index_ptr_->SetVectorIndex(index);
--------VectorIndex::SetVectorIndex
----------index_ptr_ = index_ptr;
--auto status = segment_writer_ptr->WriteVectorIndex(location_);
----SegmentWriter::WriteVectorIndex
------fs_ptr_->operation_ptr_->CreateDirectory();
------default_codec.GetVectorIndexFormat()->write(fs_ptr_, location, segment_ptr_->vector_index_ptr_);
--------DefaultVectorIndexFormat::write
```