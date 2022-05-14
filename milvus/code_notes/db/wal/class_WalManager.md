#1.class WalManager

```cpp
class WalManager {
 public:
    explicit WalManager(const MXLogConfiguration& config);
    ~WalManager();

    /*
     * init
     * @param meta
     * @retval error_code
     */
    ErrorCode
    Init(const meta::MetaPtr& meta);

    /*
     * Get next recovery
     * @param record[out]: record
     * @retval error_code
     */
    ErrorCode
    GetNextRecovery(MXLogRecord& record);

    ErrorCode
    GetNextEntityRecovery(MXLogRecord& record);

    /*
     * Get next record
     * @param record[out]: record
     * @retval error_code
     */
    ErrorCode
    GetNextRecord(MXLogRecord& record);

    ErrorCode
    GetNextEntityRecord(MXLogRecord& record);

    /*
     * Create collection
     * @param collection_id: collection id
     * @retval lsn
     */
    uint64_t
    CreateCollection(const std::string& collection_id);

    /*
     * Create partition
     * @param collection_id: collection id
     * @param partition_tag: partition tag
     * @retval lsn
     */
    uint64_t
    CreatePartition(const std::string& collection_id, const std::string& partition_tag);

    /*
     * Create hybrid collection
     * @param collection_id: collection id
     * @retval lsn
     */
    uint64_t
    CreateHybridCollection(const std::string& collection_id);

    /*
     * Drop collection
     * @param collection_id: collection id
     * @retval none
     */
    void
    DropCollection(const std::string& collection_id);

    /*
     * Drop partition
     * @param collection_id: collection id
     * @param partition_tag: partition tag
     * @retval none
     */
    void
    DropPartition(const std::string& collection_id, const std::string& partition_tag);

    /*
     * Collection is flushed (update flushed_lsn)
     * @param collection_id: collection id
     * @param lsn: flushed lsn
     */
    void
    CollectionFlushed(const std::string& collection_id, uint64_t lsn);

    /*
     * Partition is flushed (update flushed_lsn)
     * @param collection_id: collection id
     * @param partition_tag: partition_tag
     * @param lsn: flushed lsn
     */
    void
    PartitionFlushed(const std::string& collection_id, const std::string& partition_tag, uint64_t lsn);

    /*
     * Collection is updated (update wal_lsn)
     * @param collection_id: collection id
     * @param partition_tag: partition_tag
     * @param lsn: flushed lsn
     */
    void
    CollectionUpdated(const std::string& collection_id, uint64_t lsn);

    /*
     * Partition is updated (update wal_lsn)
     * @param collection_id: collection id
     * @param partition_tag: partition_tag
     * @param lsn: flushed lsn
     */
    void
    PartitionUpdated(const std::string& collection_id, const std::string& partition_tag, uint64_t lsn);

    /*
     * Insert
     * @param collection_id: collection id
     * @param collection_id: partition tag
     * @param vector_ids: vector ids
     * @param vectors: vectors
     */
    template <typename T>
    bool
    Insert(const std::string& collection_id, const std::string& partition_tag, const IDNumbers& vector_ids,
           const std::vector<T>& vectors);

    /*
     * Insert
     * @param collection_id: collection id
     * @param partition_tag: partition tag
     * @param vector_ids: vector ids
     * @param vectors: vectors
     * @param attrs: attributes
     */
    template <typename T>
    bool
    InsertEntities(const std::string& collection_id, const std::string& partition_tag,
                   const milvus::engine::IDNumbers& entity_ids, const std::vector<T>& vectors,
                   const std::unordered_map<std::string, uint64_t>& attr_nbytes,
                   const std::unordered_map<std::string, std::vector<uint8_t>>& attrs);

    /*
     * Insert
     * @param collection_id: collection id
     * @param vector_ids: vector ids
     */
    bool
    DeleteById(const std::string& collection_id, const IDNumbers& vector_ids);

    /*
     * Get flush lsn
     * @param collection_id: collection id (empty means all tables)
     * @retval if there is something not flushed, return lsn;
     *         else, return 0
     */
    uint64_t
    Flush(const std::string& collection_id = "");

    void
    RemoveOldFiles(uint64_t flushed_lsn);

 private:
    WalManager
    operator=(WalManager&);

    MXLogConfiguration mxlog_config_;

    MXLogBufferPtr p_buffer_;
    MXLogMetaHandlerPtr p_meta_handler_;

    struct TableLsn {
        uint64_t flush_lsn;
        uint64_t wal_lsn;
    };
    std::mutex mutex_;
    std::map<std::string, std::map<std::string, TableLsn>> collections_;
    std::atomic<uint64_t> last_applied_lsn_;

    // if multi-thread call Flush(), use list
    struct FlushInfo {
        std::string collection_id_;
        uint64_t lsn_ = 0;

        bool
        IsValid() {
            return (lsn_ != 0);
        }
        void
        Clear() {
            lsn_ = 0;
        }
    };
    FlushInfo flush_info_;
};

```