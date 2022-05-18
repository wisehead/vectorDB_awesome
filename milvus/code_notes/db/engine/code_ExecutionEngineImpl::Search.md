#1.ExecutionEngineImpl::Search

```
ExecutionEngineImpl::Search
--auto adapter = knowhere::AdapterMgr::GetInstance().GetAdapter(index_->index_type());
--adapter->CheckSearch(conf, index_->index_type(), index_->index_mode()))
----HNSWConfAdapter::CheckSearch
--if (hybrid) {
----HybridLoad();
------ExecutionEngineImpl::HybridLoad
--auto dataset = knowhere::GenDataset(n, index_->Dim(), data);
--auto result = index_->Query(dataset, conf);
----IndexHNSW::Query
```