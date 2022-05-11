#1.SegmentReader::LoadDeletedDocs

```
SegmentReader::LoadDeletedDocs
--fs_ptr_->operation_ptr_->CreateDirectory();
--default_codec.GetDeletedDocsFormat()->read(fs_ptr_, deleted_docs_ptr);
----DefaultDeletedDocsFormat::read
```