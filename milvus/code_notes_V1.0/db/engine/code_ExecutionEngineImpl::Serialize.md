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
--index_->UpdateIndexSize();
----CPUSPTAGRNG::UpdateIndexSize
------index_size_ = index_ptr_->GetIndexSize();
```