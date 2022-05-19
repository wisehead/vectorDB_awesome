#1.DefaultIdBloomFilterFormat::read

```
DefaultIdBloomFilterFormat::read
--std::string bloom_filter_file_path = dir_path + "/" + bloom_filter_filename_;
--scaling_bloom_t* bloom_filter =
        new_scaling_bloom_from_file(bloom_filter_capacity, bloom_filter_error_rate, bloom_filter_file_path.c_str());
----new_scaling_bloom_from_file
```