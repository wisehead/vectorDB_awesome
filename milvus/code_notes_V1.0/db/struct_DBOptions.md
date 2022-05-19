#1.struct DBOptions

```cpp
struct DBOptions {
    typedef enum { SINGLE = 0, CLUSTER_READONLY, CLUSTER_WRITABLE } MODE;

    uint16_t merge_trigger_number_ = 2;
    DBMetaOptions meta_;
    int mode_ = MODE::SINGLE;

    size_t insert_buffer_size_ = 4 * GB;
    bool insert_cache_immediately_ = false;

    int64_t auto_flush_interval_ = 1;
    int64_t file_cleanup_timeout_ = 10;

    bool metric_enable_ = false;

    // wal relative configurations
    bool wal_enable_ = true;
    bool recovery_error_ignore_ = true;
    int64_t buffer_size_ = 256;
    std::string mxlog_path_ = "/tmp/milvus/wal/";
};  // Options
```

#2.struct DBMetaOptions

```cpp
struct DBMetaOptions {
    std::string path_;
    std::vector<std::string> slave_paths_;
    std::string backend_uri_;
    ArchiveConf archive_conf_ = ArchiveConf("delete");
};  // DBMetaOptions

```

#3.struct ArchiveConf

```cpp
struct ArchiveConf {
    using CriteriaT = std::map<std::string, int64_t>;

    explicit ArchiveConf(const std::string& type, const std::string& criterias = std::string());

    const std::string&
    GetType() const {
        return type_;
    }

    const CriteriaT
    GetCriterias() const {
        return criterias_;
    }

    void
    SetCriterias(const ArchiveConf::CriteriaT& criterial);

 private:
    void
    ParseCritirias(const std::string& criterias);
    void
    ParseType(const std::string& type);

    std::string type_;
    CriteriaT criterias_;
};

```