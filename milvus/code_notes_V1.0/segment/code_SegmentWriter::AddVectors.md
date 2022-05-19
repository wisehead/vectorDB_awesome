#1.SegmentWriter::AddVectors

```
SegmentWriter::AddVectors
--segment_ptr_->vectors_ptr_->AddData(data, size);
----Vectors::AddData
------int64_t old_size = data_.size();
------data_.resize(data_.size() + size);
------memcpy(data_.data() + old_size, data, size);
--segment_ptr_->vectors_ptr_->AddUids(uids);
----Vectors::AddUids
------uids_.reserve(uids_.size() + uids.size());
------uids_.insert(uids_.end(), std::make_move_iterator(uids.begin()), std::make_move_iterator(uids.end()));
--segment_ptr_->vectors_ptr_->SetName(name);
```