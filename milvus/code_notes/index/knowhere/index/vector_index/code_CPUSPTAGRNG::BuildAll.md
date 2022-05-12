#1.CPUSPTAGRNG::BuildAll

```
CPUSPTAGRNG::BuildAll
--SetParameters(train_config);                                                           
--DatasetPtr dataset = origin;                                                           
--auto vectorset = ConvertToVectorSet(dataset);
----ConvertToVectorSet
------GETTENSOR(dataset_ptr);
--------int64_t dim = dataset_ptr->Get<int64_t>(meta::DIM);   \
        int64_t rows = dataset_ptr->Get<int64_t>(meta::ROWS); \
        const void* p_data = dataset_ptr->Get<const void*>(meta::TENSOR);
------size_t num_bytes = rows * dim * sizeof(float);
------SPTAG::ByteArray byte_array((uint8_t*)p_data, num_bytes, false);
------auto vectorset = std::make_shared<SPTAG::BasicVectorSet>(byte_array, SPTAG::VectorValueType::Float, dim, rows);        
--auto metaset = ConvertToMetadataSet(dataset);
--index_ptr_->BuildIndex(vectorset, metaset);  

```