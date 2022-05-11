#1.class DeletedDocsFormat


```cpp
class DeletedDocsFormat {
 public:
    virtual void
    read(const storage::FSHandlerPtr& fs_ptr, segment::DeletedDocsPtr& deleted_docs) = 0;

    virtual void
    write(const storage::FSHandlerPtr& fs_ptr, const segment::DeletedDocsPtr& deleted_docs) = 0;

    virtual void
    readSize(const storage::FSHandlerPtr& fs_ptr, size_t& size) = 0;
};
```