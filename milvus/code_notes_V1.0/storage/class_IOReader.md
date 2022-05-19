#1.class IOReader

```cpp
class IOReader {
 public:
    virtual bool
    open(const std::string& name) = 0;

    virtual void
    read(void* ptr, int64_t size) = 0;

    virtual void
    seekg(int64_t pos) = 0;

    virtual int64_t
    length() = 0;

    virtual void
    close() = 0;
};
```