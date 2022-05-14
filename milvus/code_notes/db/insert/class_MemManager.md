#1.class MemManager

```cpp
class MemManager {
 public:
    virtual Status
    InsertVectors(const std::string& collection_id, int64_t length, const IDNumber* vector_ids, int64_t dim,
                  const float* vectors, uint64_t lsn) = 0;

    virtual Status
    InsertVectors(const std::string& collection_id, int64_t length, const IDNumber* vector_ids, int64_t dim,
                  const uint8_t* vectors, uint64_t lsn) = 0;

    virtual Status
    InsertEntities(const std::string& collection_id, int64_t length, const IDNumber* vector_ids, int64_t dim,
                   const float* vectors, const std::unordered_map<std::string, uint64_t>& attr_nbytes,
                   const std::unordered_map<std::string, uint64_t>& attr_size,
                   const std::unordered_map<std::string, std::vector<uint8_t>>& attr_data, uint64_t lsn) = 0;

    virtual Status
    DeleteVector(const std::string& collection_id, IDNumber vector_id, uint64_t lsn) = 0;

    virtual Status
    DeleteVectors(const std::string& collection_id, int64_t length, const IDNumber* vector_ids, uint64_t lsn) = 0;

    virtual Status
    Flush(const std::string& collection_id) = 0;

    virtual Status

    Flush(std::set<std::string>& collection_ids) = 0;

    //    virtual Status
    //    Serialize(std::set<std::string>& table_ids) = 0;

    virtual Status
    EraseMemVector(const std::string& collection_id) = 0;

    virtual size_t
    GetCurrentMutableMem() = 0;

    virtual size_t
    GetCurrentImmutableMem() = 0;

    virtual size_t
    GetCurrentMem() = 0;
};  // MemManagerAbstract

```
