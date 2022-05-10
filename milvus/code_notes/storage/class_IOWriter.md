#1.class IOWriter

```cpp
class IOWriter {
 public:
    virtual bool
    open(const std::string& name) = 0;

    virtual void
    write(void* ptr, int64_t size) = 0;

    virtual int64_t
    length() = 0;

    virtual void
    close() = 0;
};
```