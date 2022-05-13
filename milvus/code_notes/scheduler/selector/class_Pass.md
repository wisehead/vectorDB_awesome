#1.class Pass

```cpp
class Pass {
 public:
    virtual void
    Init() = 0;

    virtual bool
    Run(const TaskPtr& task) = 0;
};
```