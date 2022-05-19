#1.SegmentReader::Load

```
SegmentReader::Load
--codec::DefaultCodec default_codec;
--fs_ptr_->operation_ptr_->CreateDirectory();
----DiskOperation::CreateDirectory
------is_dir = boost::filesystem::is_directory(dir_path_);
------ret = boost::filesystem::create_directory(dir_path_);
--default_codec.GetVectorsFormat()->read(fs_ptr_, segment_ptr_->vectors_ptr_);
----DefaultVectorsFormat::read
--default_codec.GetAttrsFormat()->read(fs_ptr_, segment_ptr_->attrs_ptr_);
----DefaultAttrsFormat::read
--default_codec.GetDeletedDocsFormat()->read(fs_ptr_, segment_ptr_->deleted_docs_ptr_);
```