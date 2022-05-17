#1.DBImpl::StartMetricTask

```
DBImpl::StartMetricTask
--int64_t cache_usage = cache::CpuCacheMgr::GetInstance()->CacheUsage();
----Cache::usage
--int64_t cache_total = cache::CpuCacheMgr::GetInstance()->CacheCapacity();
----CacheMgr<ItemObj>::CacheCapacity
------Cache::capacity
--server::Metrics::GetInstance().CpuCacheUsageGaugeSet(cache_usage_double * 100 / cache_total);
--server::Metrics::GetInstance().GpuCacheUsageGaugeSet();
    server::Metrics::GetInstance().DataFileSizeGaugeSet(size);
    server::Metrics::GetInstance().CPUUsagePercentSet();
    server::Metrics::GetInstance().RAMUsagePercentSet();
    server::Metrics::GetInstance().GPUPercentGaugeSet();
    server::Metrics::GetInstance().GPUMemoryUsageGaugeSet();
    server::Metrics::GetInstance().OctetsSet();

    server::Metrics::GetInstance().CPUCoreUsagePercentSet();
    server::Metrics::GetInstance().GPUTemperature();
    server::Metrics::GetInstance().CPUTemperature();
    server::Metrics::GetInstance().PushToGateway();
```