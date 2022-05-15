#1.DefaultAttrsFormat::write

```
DefaultAttrsFormat::write
--std::string dir_path = fs_ptr->operation_ptr_->GetDirectory();
--for (; it != attrs_ptr->attrs.end(); it++) {
----const std::string ra_file_path = dir_path + "/" + it->second->GetName() + raw_attr_extension_;
----int ra_fd = open(ra_file_path.c_str(), O_WRONLY | O_TRUNC | O_CREAT, 00664);
----size_t ra_num_bytes = it->second->GetNbytes();
----::write(ra_fd, &ra_num_bytes, sizeof(size_t))
----::write(ra_fd, it->second->GetData().data(), ra_num_bytes
----::close(ra_fd)
```