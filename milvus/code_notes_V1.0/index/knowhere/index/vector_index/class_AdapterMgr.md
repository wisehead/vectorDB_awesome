#1.class AdapterMgr

```cpp
class AdapterMgr {
 protected:
    bool init_ = false;
    std::unordered_map<IndexType, std::function<ConfAdapterPtr()>> collection_;
};
```