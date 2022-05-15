#1.SegmentWriter::Serialize

```
SegmentWriter::Serialize
--status = WriteBloomFilter();
----SegmentWriter::WriteBloomFilter
--status = WriteVectors();
----SegmentWriter::WriteVectors
------default_codec.GetVectorsFormat()->write(fs_ptr_, segment_ptr_->vectors_ptr_);
--------DefaultVectorsFormat::write
--status = WriteAttrs();
--// Write an empty deleted doc
--status = WriteDeletedDocs();
```