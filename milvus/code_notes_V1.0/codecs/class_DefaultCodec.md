#1.class DefaultCodec

```cpp
class DefaultCodec : public Codec {
 public:
    DefaultCodec();

    VectorsFormatPtr
    GetVectorsFormat() override;

    AttrsFormatPtr
    GetAttrsFormat() override;

    VectorIndexFormatPtr
    GetVectorIndexFormat() override;

    DeletedDocsFormatPtr
    GetDeletedDocsFormat() override;

    IdBloomFilterFormatPtr
    GetIdBloomFilterFormat() override;

 private:
    VectorsFormatPtr vectors_format_ptr_;
    AttrsFormatPtr attrs_format_ptr_;
    VectorIndexFormatPtr vector_index_format_ptr_;
    DeletedDocsFormatPtr deleted_docs_format_ptr_;
    IdBloomFilterFormatPtr id_bloom_filter_format_ptr_;
};
```
