#1.ExecutionEngineImpl::Load

```
ExecutionEngineImpl::Load
--//get from cache
--index_ = std::static_pointer_cast<knowhere::VecIndex>(cache::CpuCacheMgr::GetInstance()->GetIndex(location_));
--utils::GetParentPath(location_, segment_dir);
--
```