#1.Resource::RegisterSubscriber

```
Resource::RegisterSubscriber
--subscriber_ = std::move(subscriber);
```

#2.caller

```
ResourceWPtr
ResourceMgr::Add(ResourcePtr&& resource) {
    ResourceWPtr ret(resource);

    std::lock_guard<std::mutex> lck(resources_mutex_);
    if (running_) {
        LOG_ENGINE_ERROR_ << "ResourceMgr is running, not allow to add resource";
        return ret;
    }

    resource->RegisterSubscriber(std::bind(&ResourceMgr::post_event, this, std::placeholders::_1));

    switch (resource->type()) {
        case ResourceType::DISK: {
            disk_resources_.emplace_back(ResourceWPtr(resource));
            break;
        }
        case ResourceType::CPU: {
            cpu_resources_.emplace_back(ResourceWPtr(resource));
            break;
        }
        case ResourceType::GPU: {
            gpu_resources_.emplace_back(ResourceWPtr(resource));
            break;
        }
        case ResourceType::FPGA: {
            LOG_ENGINE_DEBUG_ << "add fpga resource";
            fpga_resources_.emplace_back(ResourceWPtr(resource));
            break;
        }
        default: { break; }
    }
    resources_.emplace_back(resource);

    return ret;
}
```