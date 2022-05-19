#1.class TaskLabel

```cpp
class TaskLabel {
 public:
    inline TaskLabelType
    Type() const {
        return type_;
    }

    virtual inline std::string
    name() const {
        return "";
    }

 protected:
    explicit TaskLabel(TaskLabelType type) : type_(type) {
    }

 private:
    TaskLabelType type_;
};
```