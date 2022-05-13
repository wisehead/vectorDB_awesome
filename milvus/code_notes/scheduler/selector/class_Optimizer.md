#1.class Optimizer

```cpp
class Optimizer {
 public:
    explicit Optimizer(std::vector<PassPtr> pass_list) : pass_list_(std::move(pass_list)) {
    }

    void
    Init();

    bool
    Run(const TaskPtr& task);

 private:
    std::vector<PassPtr> pass_list_;
};
```