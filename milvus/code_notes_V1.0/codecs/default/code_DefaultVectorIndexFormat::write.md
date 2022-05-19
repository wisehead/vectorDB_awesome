#1.DefaultVectorIndexFormat::write

```
DefaultVectorIndexFormat::write
--knowhere::VecIndexPtr index = vector_index->GetVectorIndex();
--auto binaryset = index->Serialize(knowhere::Config());
----CPUSPTAGRNG::Serialize//several index types
--int32_t index_type = knowhere::StrToOldIndexType(index->index_type());
--fs_ptr->writer_ptr_->open(location)
--fs_ptr->writer_ptr_->write(&index_type, sizeof(index_type));
--for (auto& iter : binaryset.binary_map_) {
----auto meta = iter.first.c_str();                                      
----size_t meta_length = iter.first.length();                            
----fs_ptr->writer_ptr_->write(&meta_length, sizeof(meta_length));       
----fs_ptr->writer_ptr_->write((void*)meta, meta_length);                                                                                   
----auto binary = iter.second;                                           
----int64_t binary_length = binary->size;                                
----fs_ptr->writer_ptr_->write(&binary_length, sizeof(binary_length));   
----fs_ptr->writer_ptr_->write((void*)binary->data.get(), binary_length);
--fs_ptr->writer_ptr_->close();
```