#1.class MergeManager

```cpp
class MergeManager {
 public:
    virtual MergeStrategyType
    Strategy() const = 0;

    virtual Status
    UseStrategy(MergeStrategyType type) = 0;

    virtual Status
    MergeFiles(const std::string& collection_id) = 0;
};  // MergeManager
```