#1.DefaultVectorIndexFormat::read

```
DefaultVectorIndexFormat::read
--dir_path = fs_ptr->operation_ptr_->GetDirectory();
--knowhere::VecIndexPtr index = read_internal(fs_ptr, location);
--vector_index->SetVectorIndex(index);
----
```

#2.DefaultVectorIndexFormat::read_internal

```
DefaultVectorIndexFormat::read_internal
--fs_ptr->reader_ptr_->open(path)
--length = fs_ptr->reader_ptr_->length();
--fs_ptr->reader_ptr_->seekg(0);
--fs_ptr->reader_ptr_->read(&current_type, sizeof(current_type));
--while (rp < length) {
        size_t meta_length;
        fs_ptr->reader_ptr_->read(&meta_length, sizeof(meta_length));
        rp += sizeof(meta_length);
        fs_ptr->reader_ptr_->seekg(rp);

        auto meta = new char[meta_length];
        fs_ptr->reader_ptr_->read(meta, meta_length);
        rp += meta_length;
        fs_ptr->reader_ptr_->seekg(rp);

        size_t bin_length;
        fs_ptr->reader_ptr_->read(&bin_length, sizeof(bin_length));
        rp += sizeof(bin_length);
        fs_ptr->reader_ptr_->seekg(rp);

        auto bin = new uint8_t[bin_length];
        fs_ptr->reader_ptr_->read(bin, bin_length);
        rp += bin_length;
        fs_ptr->reader_ptr_->seekg(rp);

        std::shared_ptr<uint8_t[]> binptr(bin);
        load_data_list.Append(std::string(meta, meta_length), binptr, bin_length);
        delete[] meta;
    }
--fs_ptr->reader_ptr_->close();
--index = vec_index_factory.CreateVecIndex(knowhere::OldIndexTypeToStr(current_type), knowhere::IndexMode::MODE_CPU);
--index->Load(load_data_list);
----IndexHNSW::Load//每种索引都有各自的Load函数
------auto binary = index_binary.GetByName("HNSW");
------MemoryIOReader reader;                                               
------reader.total = binary->size;                                         
------reader.data_ = binary->data.get();                                                                                                      
------hnswlib::SpaceInterface<float>* space;                               
------index_ = std::make_shared<hnswlib::HierarchicalNSW<float>>(space);   
------index_->loadIndex(reader);                                           
--index->UpdateIndexSize();
----IndexHNSW::UpdateIndexSize
------index_size_ = index_->cal_size();
--return index;
```