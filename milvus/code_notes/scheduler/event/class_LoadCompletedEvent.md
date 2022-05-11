#1.class LoadCompletedEvent

```cpp
class LoadCompletedEvent : public Event {
 public:
    LoadCompletedEvent(std::shared_ptr<Resource> resource, TaskTableItemPtr task_table_item)
        : Event(EventType::LOAD_COMPLETED, std::move(resource)), task_table_item_(std::move(task_table_item)) {
    }

    inline std::string
    Dump() const override {
        return "<LoadCompletedEvent>";
    }

    friend std::ostream&
    operator<<(std::ostream& out, const LoadCompletedEvent& event);

 public:
    TaskTableItemPtr task_table_item_;
};

```