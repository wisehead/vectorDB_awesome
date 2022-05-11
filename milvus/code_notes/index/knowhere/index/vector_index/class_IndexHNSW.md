#1.class IndexHNSW

```cpp
class IndexHNSW : public VecIndex {
 public:
    IndexHNSW() {
        index_type_ = IndexEnum::INDEX_HNSW;
    }

    BinarySet
    Serialize(const Config& config = Config()) override;

    void
    Load(const BinarySet& index_binary) override;

    void
    Train(const DatasetPtr& dataset_ptr, const Config& config) override;

    void
    AddWithoutIds(const DatasetPtr&, const Config&) override;

    DatasetPtr
    Query(const DatasetPtr& dataset_ptr, const Config& config) override;

    int64_t
    Count() override;

    int64_t
    Dim() override;

    void
    UpdateIndexSize() override;

 private:
    bool normalize = false;
    std::shared_ptr<hnswlib::HierarchicalNSW<float>> index_;
};


```