#1.DefaultAttrsFormat::read

```
DefaultAttrsFormat::read
--dir_path = fs_ptr->operation_ptr_->GetDirectory();
--boost::filesystem::path target_path(dir_path);
  typedef boost::filesystem::directory_iterator d_it;
  d_it it_end;
  d_it uid_it(target_path);
--for (; uid_it != it_end; ++uid_it) {
        const auto& path = uid_it->path();
        if (path.extension().string() == user_id_extension_) {
            read_uids_internal(fs_ptr, path.string(), uids);
            break;
        }
    }
--for (; it != it_end; ++it) {
----const auto& path = it->path();
----if (path.extension().string() == raw_attr_extension_) {
------auto file_name = path.filename().string();
      auto field_name = file_name.substr(0, file_name.size() - 3);
      std::vector<uint8_t> attr_list;
      size_t nbytes;
------read_attrs_internal(fs_ptr, path.string(), 0, INT64_MAX, attr_list, nbytes);
------milvus::segment::AttrPtr attr = std::make_shared<milvus::segment::Attr>(attr_list, nbytes, uids, field_name);
------attrs_read->attrs.insert(std::pair(field_name, attr));

```

#2. DefaultAttrsFormat::read_uids_internal

```
read_uids_internal
--open_res = fs_ptr->reader_ptr_->open(file_path.c_str());
--fs_ptr->reader_ptr_->read(&num_bytes, sizeof(size_t));
--uids.resize(num_bytes / sizeof(int64_t));
--fs_ptr->reader_ptr_->read(uids.data(), num_bytes);
--fs_ptr->reader_ptr_->read(uids.data(), num_bytes);
```

#3.DefaultAttrsFormat::read_attrs_internal

```
DefaultAttrsFormat::read_attrs_internal
--open_res = fs_ptr->reader_ptr_->open(file_path.c_str());
--fs_ptr->reader_ptr_->read(&nbytes, sizeof(size_t));
--num = std::min(num, nbytes - offset);
--offset += sizeof(size_t);
--fs_ptr->reader_ptr_->seekg(offset);
--raw_attrs.resize(num / sizeof(uint8_t));
--fs_ptr->reader_ptr_->read(raw_attrs.data(), num);
----DiskIOReader::read
--fs_ptr->reader_ptr_->close();
```