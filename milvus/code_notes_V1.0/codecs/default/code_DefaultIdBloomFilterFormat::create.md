#1.DefaultIdBloomFilterFormat::create

```
DefaultIdBloomFilterFormat::create
--std::string dir_path = fs_ptr->operation_ptr_->GetDirectory();
--const std::string bloom_filter_file_path = dir_path + "/" + bloom_filter_filename_;
--scaling_bloom_t* bloom_filter =new_scaling_bloom(bloom_filter_capacity, 		bloom_filter_error_rate, bloom_filter_file_path.c_str());
--d_bloom_filter_ptr = std::make_shared<segment::IdBloomFilter>(bloom_filter);
```