#1.class MemMetadataSet

```cpp
class MemMetadataSet : public MetadataSet
{
public:
    MemMetadataSet(ByteArray p_metadata, ByteArray p_offsets, SizeType p_count);

    ~MemMetadataSet();

    ByteArray GetMetadata(SizeType p_vectorID) const;

    SizeType Count() const;

    bool Available() const;

    std::pair<std::uint64_t, std::uint64_t> BufferSize() const;

    void AddBatch(MetadataSet& data);

    ErrorCode SaveMetadata(std::ostream& p_metaOut, std::ostream& p_metaIndexOut);

    ErrorCode SaveMetadata(const std::string& p_metaFile, const std::string& p_metaindexFile);

private:
    std::vector<std::uint64_t> m_offsets;

    SizeType m_count;

    ByteArray m_metadataHolder;

    ByteArray m_offsetHolder;

    std::vector<std::uint8_t> m_newdata;
};
```