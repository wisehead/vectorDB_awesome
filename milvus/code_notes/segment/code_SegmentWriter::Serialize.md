#1.SegmentWriter::Serialize

```
SegmentWriter::Serialize
--status = WriteBloomFilter();
----SegmentWriter::WriteBloomFilter
--status = WriteVectors();
--status = WriteAttrs();
--// Write an empty deleted doc
--status = WriteDeletedDocs();
```