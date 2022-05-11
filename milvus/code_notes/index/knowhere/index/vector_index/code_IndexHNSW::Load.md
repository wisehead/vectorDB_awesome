#1.IndexHNSW::Load

```cpp
IndexHNSW::Load
--auto binary = index_binary.GetByName("HNSW");
--MemoryIOReader reader;                                               
--reader.total = binary->size;                                         
--reader.data_ = binary->data.get();                                                                                                    
--hnswlib::SpaceInterface<float>* space;                               
--index_ = std::make_shared<hnswlib::HierarchicalNSW<float>>(space);   
--index_->loadIndex(reader);       
----HierarchicalNSW::loadIndex                                    
```