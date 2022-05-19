#1.DefaultVectorsFormat::read_uids

```
DefaultVectorsFormat::read_uids
--dir_path = fs_ptr->operation_ptr_->GetDirectory();
--boost::filesystem::path target_path(dir_path);
  typedef boost::filesystem::directory_iterator d_it;
  d_it it_end;
  d_it it(target_path);
--for (; it != it_end; ++it) {
        const auto& path = it->path();
        if (path.extension().string() == user_id_extension_) {
            read_uids_internal(fs_ptr, path.string(), uids);
            break;
        }
    }

```

#2. DefaultVectorsFormat::read_uids_internal

```
read_uids_internal
--fs_ptr->reader_ptr_->open(file_path.c_str())
--fs_ptr->reader_ptr_->read(&num_bytes, sizeof(size_t));
--fs_ptr->reader_ptr_->read(uids.data(), num_bytes);
--fs_ptr->reader_ptr_->close();
```