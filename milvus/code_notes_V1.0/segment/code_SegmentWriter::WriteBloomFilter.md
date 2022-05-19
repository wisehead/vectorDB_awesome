#1.SegmentWriter::WriteBloomFilter

```
SegmentWriter::WriteBloomFilter
--fs_ptr_->operation_ptr_->CreateDirectory();
--default_codec.GetIdBloomFilterFormat()->create(fs_ptr_, segment_ptr_->id_bloom_filter_ptr_);
--auto& uids = segment_ptr_->vectors_ptr_->GetUids();
        for (auto& uid : uids) {
            segment_ptr_->id_bloom_filter_ptr_->Add(uid);
        }
--default_codec.GetIdBloomFilterFormat()->write(fs_ptr_, segment_ptr_->id_bloom_filter_ptr_);
----DefaultIdBloomFilterFormat::write
```