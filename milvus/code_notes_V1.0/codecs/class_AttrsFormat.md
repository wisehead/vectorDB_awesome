#1.class AttrsFormat

```cpp
class AttrsFormat {
 public:
    virtual void
    read(const storage::FSHandlerPtr& fs_ptr, segment::AttrsPtr& attrs_read) = 0;

    virtual void
    write(const storage::FSHandlerPtr& fs_ptr, const segment::AttrsPtr& attr) = 0;

    virtual void
    read_uids(const storage::FSHandlerPtr& fs_ptr, std::vector<int64_t>& uids) = 0;
};
```