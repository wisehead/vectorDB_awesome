#1.class Codec

```cpp
class Codec {
 public:
    virtual VectorsFormatPtr
    GetVectorsFormat() = 0;

    virtual AttrsFormatPtr
    GetAttrsFormat() = 0;

    virtual VectorIndexFormatPtr
    GetVectorIndexFormat() = 0;

    virtual DeletedDocsFormatPtr
    GetDeletedDocsFormat() = 0;

    virtual IdBloomFilterFormatPtr
    GetIdBloomFilterFormat() = 0;

    // TODO(zhiru)
    /*
    virtual AttrsFormat
    GetAttrsFormat() = 0;

    virtual AttrsIndexFormat
    GetAttrsIndexFormat() = 0;

    virtual IdIndexFormat
    GetIdIndexFormat() = 0;

    */
};

```