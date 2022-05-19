#1.class MemManagerImpl

```cpp
class MemManagerImpl : public MemManager, public server::CacheConfigHandler {
 public:
    using Ptr = std::shared_ptr<MemManagerImpl>;
    using MemIdMap = std::map<std::string, MemTablePtr>;
    using MemList = std::vector<MemTablePtr>;

 private:
    MemIdMap mem_id_map_;
    MemList immu_mem_list_;
    meta::MetaPtr meta_;
    DBOptions options_;
    std::mutex mutex_;
    std::mutex serialization_mtx_;
};  // NewMemManager

```