#1.class ResourceMgr

```cpp
namespace milvus {
namespace scheduler {

class ResourceMgr : public interface::dumpable {
 private:
    bool running_ = false;

    std::vector<ResourceWPtr> disk_resources_;
    std::vector<ResourceWPtr> cpu_resources_;
    std::vector<ResourceWPtr> gpu_resources_;
    std::vector<ResourceWPtr> fpga_resources_;
    std::vector<ResourcePtr> resources_;
    mutable std::mutex resources_mutex_;

    std::queue<EventPtr> queue_;
    std::function<void(EventPtr)> subscriber_ = nullptr;
    std::mutex event_mutex_;
    std::condition_variable event_cv_;

    std::thread worker_thread_;
};

using ResourceMgrPtr = std::shared_ptr<ResourceMgr>;
using ResourceMgrWPtr = std::weak_ptr<ResourceMgr>;

}  // namespace scheduler
}  // namespace milvus

```