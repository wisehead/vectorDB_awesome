#1.class ConfAdapter

```cpp
class ConfAdapter {
 public:
    virtual bool
    CheckTrain(Config& oricfg, IndexMode& mode);

    virtual bool
    CheckSearch(Config& oricfg, const IndexType type, const IndexMode mode);
};
```