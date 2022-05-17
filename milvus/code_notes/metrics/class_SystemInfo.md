#1.class SystemInfo

```cpp
class SystemInfo {
 private:
    int64_t total_ram_ = 0;
    clock_t last_cpu_ = clock_t();
    clock_t last_sys_cpu_ = clock_t();
    clock_t last_user_cpu_ = clock_t();
    std::chrono::system_clock::time_point net_time_ = std::chrono::system_clock::now();
    int32_t num_processors_ = 0;
    int32_t num_physical_processors_ = 0;
    // number of GPU
    uint32_t num_device_ = 0;
    int64_t in_octets_ = 0;
    int64_t out_octets_ = 0;
    bool initialized_ = false;
};
```