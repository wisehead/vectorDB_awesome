#1.class MemTable

```cpp
class MemTable : public server::CacheConfigHandler {

 private:
    const std::string collection_id_;

    MemTableFileList mem_table_file_list_;

    meta::MetaPtr meta_;

    DBOptions options_;

    std::mutex mutex_;

    std::set<segment::doc_id_t> doc_ids_to_delete_;

    std::atomic<uint64_t> lsn_;
};  // MemTable

```