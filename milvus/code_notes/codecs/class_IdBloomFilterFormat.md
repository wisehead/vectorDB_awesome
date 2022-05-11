#1.class IdBloomFilterFormat

```cpp
class IdBloomFilterFormat {
 public:
    virtual void
    read(const storage::FSHandlerPtr& fs_ptr, segment::IdBloomFilterPtr& id_bloom_filter_ptr) = 0;

    virtual void
    write(const storage::FSHandlerPtr& fs_ptr, const segment::IdBloomFilterPtr& id_bloom_filter_ptr) = 0;

    virtual void
    create(const storage::FSHandlerPtr& fs_ptr, segment::IdBloomFilterPtr& id_bloom_filter_ptr) = 0;
};
```