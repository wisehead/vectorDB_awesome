#1.class ConfigMgr

```cpp
class ConfigMgr {
 public:
    virtual Status
    LoadConfigFile(const std::string& filename) = 0;

    virtual void
    Print() const = 0;  // will be deleted

    virtual std::string
    DumpString() const = 0;

    virtual const ConfigNode&
    GetRootNode() const = 0;

    virtual ConfigNode&
    GetRootNode() = 0;
};
```