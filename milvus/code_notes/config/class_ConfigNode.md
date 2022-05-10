#1.class ConfigNode

```cpp
class ConfigNode {
 private:
    std::map<std::string, std::string> config_;
    std::map<std::string, ConfigNode> children_;
    std::map<std::string, std::vector<std::string> > sequences_;
};

```