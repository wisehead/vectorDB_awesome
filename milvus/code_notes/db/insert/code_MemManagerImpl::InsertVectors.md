#1.MemManagerImpl::InsertVectors

```
//binary uint_
MemManagerImpl::InsertVectors
--VectorsData vectors_data;                                                         
--vectors_data.vector_count_ = length;                                              
--vectors_data.binary_data_.resize(length * dim);                                   
--memcpy(vectors_data.binary_data_.data(), vectors, length * dim * sizeof(uint8_t));
--vectors_data.id_array_.resize(length);                                            
--memcpy(vectors_data.id_array_.data(), vector_ids, length * sizeof(IDNumber));     
--VectorSourcePtr source = std::make_shared<VectorSource>(vectors_data);                                                                                              
--std::unique_lock<std::mutex> lock(mutex_);                                                                                                             
--return InsertVectorsNoLock(collection_id, source, lsn);                           

```