#1.scheduler::StartSchedulerService()

```
scheduler::StartSchedulerService()
--load_simple_config
----ResMgrInst::GetInstance()->Add(ResourceFactory::Create("disk", "DISK", 0, false));
------ResourceFactory::Create
------ResourceMgr::Add
--------ResourceMgr::post_event
----------queue_.emplace(event);
----------event_cv_.notify_one();
--------RegisterSubscriber
----------subscriber_ = std::move(subscriber);
--------switch (resource->type()) {
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
```