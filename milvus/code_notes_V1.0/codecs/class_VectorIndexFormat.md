#1.class VectorIndexFormat

```cpp
class VectorIndexFormat {
 public:
    virtual void
    read(const storage::FSHandlerPtr& fs_ptr, const std::string& location, segment::VectorIndexPtr& vector_index) = 0;

    virtual void
    write(const storage::FSHandlerPtr& fs_ptr, const std::string& location,
          const segment::VectorIndexPtr& vector_index) = 0;
};
```