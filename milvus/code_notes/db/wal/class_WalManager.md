#1.class WalManager

```cpp
class WalManager {
 private:
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