#1.ExecutionEngineImpl::Load

```
ExecutionEngineImpl::Load
--//get from cache
--index_ = std::static_pointer_cast<knowhere::VecIndex>(cache::CpuCacheMgr::GetInstance()->GetIndex(location_));
--utils::GetParentPath(location_, segment_dir);
--auto segment_reader_ptr = std::make_shared<segment::SegmentReader>(segment_dir);
----SegmentReader::SegmentReader
------storage::IOReaderPtr reader_ptr = std::make_shared<storage::DiskIOReader>();                
------storage::IOWriterPtr writer_ptr = std::make_shared<storage::DiskIOWriter>();                
------storage::OperationPtr operation_ptr = std::make_shared<storage::DiskOperation>(directory);  
------fs_ptr_ = std::make_shared<storage::FSHandler>(reader_ptr, writer_ptr, operation_ptr);      
------segment_ptr_ = std::make_shared<Segment>();                                                 
--vec_index_factory = knowhere::VecIndexFactory::GetInstance();
--if (utils::IsRawIndexType((int32_t)index_type_)) 
----if (index_type_ == EngineType::FAISS_IDMAP) 
------index_ = vec_index_factory.CreateVecIndex(knowhere::IndexEnum::INDEX_FAISS_IDMAP);
--------VecIndexFactory::CreateVecIndex
----milvus::json conf{{knowhere::meta::DEVICEID, gpu_num_}, {knowhere::meta::DIM, dim_}};
----MappingMetricType(metric_type_, conf);
----AdapterMgr::GetAdapter
------return collection_.at(type)();
----mode = index_->index_mode();
----adapter->CheckTrain(conf, mode)
------IVFConfAdapter::CheckTrain
----SegmentReader::Load
----segment_reader_ptr->GetSegment(segment_ptr);
----auto& vectors = segment_ptr->vectors_ptr_;
    auto& deleted_docs = segment_ptr->deleted_docs_ptr_->GetDeletedDocs();
----vectors_uids = vectors->GetMutableUids();
------Vectors::GetMutableUids
----vector_uids_ptr->swap(vectors_uids);
----auto& vectors_data = vectors->GetData();
----auto attrs = segment_ptr->attrs_ptr_;
----auto attrs_it = attrs->attrs.begin();
----for (; attrs_it != attrs->attrs.end(); ++attrs_it) {
                attr_data_.insert(std::pair(attrs_it->first, attrs_it->second->GetData()));
                attr_size_.insert(std::pair(attrs_it->first, attrs_it->second->GetNbytes()));
            }
----auto count = vector_uids_ptr->size();
----vector_count_ = count;
----if (!deleted_docs.empty()) {
------concurrent_bitset_ptr = std::make_shared<faiss::ConcurrentBitset>(count);
------for (auto& offset : deleted_docs) {
--------concurrent_bitset_ptr->set(offset);
----auto dataset = knowhere::GenDataset(count, this->dim_, vectors_data.data());   
```