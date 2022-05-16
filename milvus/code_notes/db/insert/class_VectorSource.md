#1.class VectorSource

```cpp
class VectorSource {
 private:
    VectorsData vectors_;
    IDNumbers vector_ids_;
    const std::unordered_map<std::string, uint64_t> attr_nbytes_;
    std::unordered_map<std::string, uint64_t> attr_size_;
    std::unordered_map<std::string, std::vector<uint8_t>> attr_data_;

    size_t current_num_vectors_added;
    size_t current_num_attrs_added;
};  // VectorSource
```