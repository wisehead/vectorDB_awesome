#1.class DiskIOWriter

```cpp
class DiskIOWriter : public IOWriter {
 public:
    std::string name_;
    int64_t len_;
    std::fstream fs_;
};

```