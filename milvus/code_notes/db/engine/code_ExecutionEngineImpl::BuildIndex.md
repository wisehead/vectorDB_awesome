#1.ExecutionEngineImpl::BuildIndex

```
ExecutionEngineImpl::BuildIndex
--auto from_index = std::dynamic_pointer_cast<knowhere::IDMAP>(index_);
--auto bin_from_index = std::dynamic_pointer_cast<knowhere::BinaryIDMAP>(index_);
--milvus::json conf = index_params_;
    conf[knowhere::meta::DIM] = Dimension();
    conf[knowhere::meta::ROWS] = Count();
    conf[knowhere::meta::DEVICEID] = gpu_num_;
--auto adapter = knowhere::AdapterMgr::GetInstance().GetAdapter(MappingIndexType(engine_type));
--mode = GetModeFromConfig();
--adapter->CheckTrain(conf, mode)
--auto to_index = CreatetVecIndex(engine_type, mode);
----ExecutionEngineImpl::CreatetVecIndex
--if (from_index)
----auto dataset = knowhere::GenDataset(Count(), Dimension(), from_index->GetRawVectors());
----to_index->BuildAll(dataset, conf);//all kinds of buildAll
------CPUSPTAGRNG::BuildAll//
--------SetParameters(train_config);
--------DatasetPtr dataset = origin;
--else if (bin_from_index)
----
```