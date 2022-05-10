#1.class Resource

```cpp
class Resource : public Node, public std::enable_shared_from_this<Resource> {
 protected:
    uint64_t device_id_;
    std::string name_;

 private:
    ResourceType type_;

    TaskTable task_table_;

    uint64_t total_cost_ = 0;
    uint64_t total_task_ = 0;

    std::function<void(EventPtr)> subscriber_ = nullptr;

    bool running_ = false;
    bool enable_executor_ = true;
    std::thread loader_thread_;
    std::thread executor_thread_;

    bool load_flag_ = false;
    bool exec_flag_ = false;
    std::mutex load_mutex_;
    std::mutex exec_mutex_;
    std::condition_variable load_cv_;
    std::condition_variable exec_cv_;
};

```