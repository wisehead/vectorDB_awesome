#1.IDMAP::Train

```
IDMAP::Train
--int64_t dim = config[meta::DIM].get<int64_t>();                                           
--faiss::MetricType metric_type = GetMetricType(config[Metric::TYPE].get<std::string>());   
--auto index = std::make_shared<faiss::IndexFlat>(dim, metric_type);                        
--index_ = index;//FaissBaseIndex.index_                                                                           

```