#1.class SpecResLabel

```cpp
class SpecResLabel : public TaskLabel {
 public:
    explicit SpecResLabel(const ResourceWPtr& resource, bool hybrid = false)
        : TaskLabel(TaskLabelType::SPECIFIED_RESOURCE), resource_(resource), hybrid_(hybrid) {
    }

    ResourceWPtr&
    resource() {
        return resource_;
    }

    std::string
    name() const override {
        return resource_.lock()->name();
    }

    bool
    IsHybrid() {
        return hybrid_;
    }

 private:
    bool hybrid_;
    ResourceWPtr resource_;
};
```