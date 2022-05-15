#1.DefaultVectorsFormat::write

```
DefaultVectorsFormat::write
--std::string dir_path = fs_ptr->operation_ptr_->GetDirectory();
--const std::string rv_file_path = dir_path + "/" + vectors->GetName() + raw_vector_extension_;
--const std::string uid_file_path = dir_path + "/" + vectors->GetName() + user_id_extension_;
--DiskIOWriter::open
--size_t rv_num_bytes = vectors->GetData().size() * sizeof(uint8_t);
  fs_ptr->writer_ptr_->write(&rv_num_bytes, sizeof(size_t));
  fs_ptr->writer_ptr_->write((void*)vectors->GetData().data(), rv_num_bytes);
  fs_ptr->writer_ptr_->close();
--fs_ptr->writer_ptr_->open(uid_file_path.c_str())
--size_t uid_num_bytes = vectors->GetUids().size() * sizeof(segment::doc_id_t);
    fs_ptr->writer_ptr_->write(&uid_num_bytes, sizeof(size_t));
    fs_ptr->writer_ptr_->write((void*)vectors->GetUids().data(), uid_num_bytes);
    fs_ptr->writer_ptr_->close();
```