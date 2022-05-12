#1.CPUSPTAGRNG::BuildAll

```
CPUSPTAGRNG::BuildAll
--SetParameters(train_config);                                                           
--DatasetPtr dataset = origin;                                                           
--auto vectorset = ConvertToVectorSet(dataset);
----ConvertToVectorSet      
--auto metaset = ConvertToMetadataSet(dataset);
----ConvertToMetadataSet
--index_ptr_->BuildIndex(vectorset, metaset);  
----VectorIndex::BuildIndex//SPTAG_VectorIndex
------BuildIndex(p_vectorSet->GetData(), p_vectorSet->Count(), p_vectorSet->Dimension());
--------Index<T>::BuildIndex//BKT
--------Index<T>::BuildIndex//KDT
------m_pMetadata = std::move(p_metadataSet);
------if (p_withMetaIndex && m_pMetadata != nullptr) 
          BuildMetaMapping();


```

#2. ConvertToVectorSet
```
ConvertToVectorSet
--GETTENSOR(dataset_ptr);
----int64_t dim = dataset_ptr->Get<int64_t>(meta::DIM);   \
        int64_t rows = dataset_ptr->Get<int64_t>(meta::ROWS); \
        const void* p_data = dataset_ptr->Get<const void*>(meta::TENSOR);
--size_t num_bytes = rows * dim * sizeof(float);
--SPTAG::ByteArray byte_array((uint8_t*)p_data, num_bytes, false);
--auto vectorset = std::make_shared<SPTAG::BasicVectorSet>(byte_array, SPTAG::VectorValueType::Float, dim, rows);  
```

#3.ConvertToMetadataSet
```
ConvertToMetadataSet
--auto elems = dataset_ptr->Get<int64_t>(meta::ROWS);
--auto p_id = (int64_t*)malloc(sizeof(int64_t) * elems);
--for (int64_t i = 0; i < elems; ++i) p_id[i] = i;

--auto p_offset = (int64_t*)malloc(sizeof(int64_t) * (elems + 1));
--for (int64_t i = 0; i <= elems; ++i) p_offset[i] = i * 8;

--std::shared_ptr<SPTAG::MetadataSet> metaset(
        new SPTAG::MemMetadataSet(SPTAG::ByteArray((std::uint8_t*)p_id, elems * sizeof(int64_t), true),
                                  SPTAG::ByteArray((std::uint8_t*)p_offset, elems * sizeof(int64_t), true), elems));
```