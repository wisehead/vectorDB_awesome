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
```