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
----
```