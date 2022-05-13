#1.class FallbackPass

```cpp

class FallbackPass : public Pass {
 public:
    FallbackPass() = default;

 public:
    void
    Init() override;

    bool
    Run(const TaskPtr& task) override;
};

```