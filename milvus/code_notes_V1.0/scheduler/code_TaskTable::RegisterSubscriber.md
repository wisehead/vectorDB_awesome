#1.TaskTable::RegisterSubscriber

```cpp
inline void
    RegisterSubscriber(std::function<void(void)> subscriber) {
        subscriber_ = std::move(subscriber);
    }
```

#2.caller Resource::Resource

```cpp
Resource::Resource(std::string name, ResourceType type, uint64_t device_id, bool enable_executor)
    : device_id_(device_id), name_(std::move(name)), type_(type), enable_executor_(enable_executor) {
    // register subscriber in tasktable
    task_table_.RegisterSubscriber([&] {
        if (subscriber_) {
            auto event = std::make_shared<TaskTableUpdatedEvent>(shared_from_this());
            subscriber_(std::static_pointer_cast<Event>(event));
        }
    });
}
```