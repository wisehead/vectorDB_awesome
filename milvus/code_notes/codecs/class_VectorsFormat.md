#1.class VectorsFormat

```cpp
class VectorsFormat {
 public:
    virtual void
    read(const storage::FSHandlerPtr& fs_ptr, segment::VectorsPtr& vectors_read) = 0;

    virtual void
    write(const storage::FSHandlerPtr& fs_ptr, const segment::VectorsPtr& vectors) = 0;

    virtual void
    read_uids(const storage::FSHandlerPtr& fs_ptr, std::vector<segment::doc_id_t>& uids) = 0;

    virtual void
    read_vectors(const storage::FSHandlerPtr& fs_ptr, off_t offset, size_t num_bytes,
                 std::vector<uint8_t>& raw_vectors) = 0;
};
```