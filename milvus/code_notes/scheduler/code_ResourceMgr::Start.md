#1.ResourceMgr::Start

```
ResourceMgr::Start
--std::lock_guard<std::mutex> lck(resources_mutex_);
--for (auto& resource : resources_) 
----resource->Start();
--running_ = true;
--worker_thread_ = std::thread(&ResourceMgr::event_process, this);
```