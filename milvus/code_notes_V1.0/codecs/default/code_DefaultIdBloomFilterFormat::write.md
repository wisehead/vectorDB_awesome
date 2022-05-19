#1.DefaultIdBloomFilterFormat::write

```
DefaultIdBloomFilterFormat::write
--std::string dir_path = fs_ptr->operation_ptr_->GetDirectory();
--const std::string bloom_filter_file_path = dir_path + "/" + bloom_filter_filename_;
--scaling_bloom_flush(id_bloom_filter_ptr->GetBloomFilter())
```