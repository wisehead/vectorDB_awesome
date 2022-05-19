#1.DefaultVectorsFormat::read

```
DefaultVectorsFormat::read
--dir_path = fs_ptr->operation_ptr_->GetDirectory();
--boost::filesystem::path target_path(dir_path);
  typedef boost::filesystem::directory_iterator d_it;
  d_it it_end;
  d_it it(target_path);
--for (; it != it_end; ++it) 
----path = it->path();
----if (path.extension().string() == raw_vector_extension_)
------vector_list = vectors_read->GetMutableData();
------read_vectors_internal(fs_ptr, path.string(), 0, INT64_MAX, vector_list);

```

#2. DefaultVectorsFormat::read_vectors_internal

```
DefaultVectorsFormat::read_vectors_internal
--fs_ptr->reader_ptr_->open(file_path.c_str())
--fs_ptr->reader_ptr_->read(&num_bytes, sizeof(size_t));
--num = std::min(num, num_bytes - offset);
--fs_ptr->reader_ptr_->seekg(offset);
--raw_vectors.resize(num / sizeof(uint8_t));
--fs_ptr->reader_ptr_->read(raw_vectors.data(), num);
--fs_ptr->reader_ptr_->close();
```