#1.class YamlConfigMgr

```cpp
class YamlConfigMgr : public ConfigMgr {
 private:
    YAML::Node node_;
    ConfigNode config_;
};
```