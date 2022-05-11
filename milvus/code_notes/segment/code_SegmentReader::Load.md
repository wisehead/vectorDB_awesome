#1.SegmentReader::Load

```
SegmentReader::Load
--codec::DefaultCodec default_codec;
--fs_ptr_->operation_ptr_->CreateDirectory();
----DiskOperation::CreateDirectory
------is_dir = boost::filesystem::is_directory(dir_path_);
------ret = boost::filesystem::create_directory(dir_path_);
```