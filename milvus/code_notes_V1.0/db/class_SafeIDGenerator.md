#1.class SafeIDGenerator

```cpp
class SafeIDGenerator : public IDGenerator {
 public:
    static SafeIDGenerator&
    GetInstance() {
        static SafeIDGenerator instance;
        return instance;
    }

    ~SafeIDGenerator() override = default;

    IDNumber
    GetNextIDNumber() override;

    Status
    GetNextIDNumbers(size_t n, IDNumbers& ids) override;

 private:
    SafeIDGenerator() = default;

    Status
    NextIDNumbers(size_t n, IDNumbers& ids);

    static constexpr size_t MAX_IDS_PER_MICRO = 1000;

    std::mutex mtx_;
    int64_t time_stamp_ms_ = 0;
};
```