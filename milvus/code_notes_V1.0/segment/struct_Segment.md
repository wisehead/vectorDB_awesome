#1.struct Segment

```cpp
struct Segment {
    VectorsPtr vectors_ptr_ = std::make_shared<Vectors>();
    AttrsPtr attrs_ptr_ = std::make_shared<Attrs>();
    VectorIndexPtr vector_index_ptr_ = std::make_shared<VectorIndex>();
    DeletedDocsPtr deleted_docs_ptr_ = nullptr;
    IdBloomFilterPtr id_bloom_filter_ptr_ = nullptr;
};
```