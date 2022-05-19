#1.struct MXLogRecordHeader

```cpp
struct MXLogRecordHeader {
    uint64_t mxl_lsn;  // log sequence number (high 32 bits: file No. inc by 1, low 32 bits: offset in file, max 4GB)
    uint8_t mxl_type;  // record type, insert/delete/update/flush...
    uint16_t collection_id_size;
    uint16_t partition_tag_size;
    uint32_t vector_num;
    uint32_t data_size;
};

```