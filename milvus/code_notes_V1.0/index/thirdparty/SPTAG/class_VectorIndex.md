#1.class VectorIndex

```cpp
namespace SPTAG
{

class VectorIndex
{
protected:
    std::string m_sIndexName;
    std::string m_sMetadataFile = "metadata.bin";
    std::string m_sMetadataIndexFile = "metadataIndex.bin";
    std::shared_ptr<MetadataSet> m_pMetadata;
    std::unique_ptr<std::unordered_map<std::string, SizeType>> m_pMetaToVec;
};


} // namespace SPTAG


```