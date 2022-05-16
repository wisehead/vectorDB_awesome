#1.MemManagerImpl::InsertEntities

```
MemManagerImpl::InsertEntities
--VectorsData vectors_data;                                                                                  
--vectors_data.vector_count_ = length;                                                                       
--vectors_data.float_data_.resize(length * dim);                                                             
--memcpy(vectors_data.float_data_.data(), vectors, length * dim * sizeof(float));                            
--vectors_data.id_array_.resize(length);                                                                     
--memcpy(vectors_data.id_array_.data(), vector_ids, length * sizeof(IDNumber));                                                                                                                                
--VectorSourcePtr source = std::make_shared<VectorSource>(vectors_data, attr_nbytes, attr_size, attr_data);                                                                                                             
--std::unique_lock<std::mutex> lock(mutex_);                                                                                                                                                                            
--return InsertEntitiesNoLock(collection_id, source, lsn);                                                   


```