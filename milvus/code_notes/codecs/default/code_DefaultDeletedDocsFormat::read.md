#1.DefaultDeletedDocsFormat::read

```
DefaultDeletedDocsFormat::read
--dir_path = fs_ptr->operation_ptr_->GetDirectory();
--del_file_path = dir_path + "/" + deleted_docs_filename_;
--del_fd = open(del_file_path.c_str(), O_RDONLY, 00664);
--::read(del_fd, &num_bytes, sizeof(size_t))
--auto deleted_docs_size = num_bytes / sizeof(segment::offset_t);
--std::vector<segment::offset_t> deleted_docs_list;
--deleted_docs_list.resize(deleted_docs_size);
--::read(del_fd, deleted_docs_list.data(), num_bytes)
--deleted_docs = std::make_shared<segment::DeletedDocs>(deleted_docs_list);
--::close(del_fd)
```