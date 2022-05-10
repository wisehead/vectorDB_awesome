#1.Config

```cpp

class Config {
 private:
    bool restart_required_ = false;
    std::string config_file_;
    std::unordered_map<std::string, std::unordered_map<std::string, std::string>> config_map_;
    std::unordered_map<std::string, std::unordered_map<std::string, ConfigCallBackF>> config_callback_;
    std::mutex callback_mutex_;
    std::mutex mutex_;
};

}  // namespace server
}  // namespace milvus

```