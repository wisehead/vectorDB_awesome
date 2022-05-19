#1.class BinaryIDMAP

```cpp
class BinaryIDMAP : public VecIndex, public FaissBaseBinaryIndex {
 public:
    BinaryIDMAP() : FaissBaseBinaryIndex(nullptr) {
        index_type_ = IndexEnum::INDEX_FAISS_BIN_IDMAP;
    }

    explicit BinaryIDMAP(std::shared_ptr<faiss::IndexBinary> index) : FaissBaseBinaryIndex(std::move(index)) {
        index_type_ = IndexEnum::INDEX_FAISS_BIN_IDMAP;
    }

    BinarySet
    Serialize(const Config& config = Config()) override;

    void
    Load(const BinarySet& index_binary) override;

    void
    Train(const DatasetPtr&, const Config&) override;

    void
    AddWithoutIds(const DatasetPtr&, const Config&) override;

    DatasetPtr
    Query(const DatasetPtr&, const Config&) override;

    int64_t
    Count() override;

    int64_t
    Dim() override;

    int64_t
    IndexSize() override {
        return Count() * Dim() / 8;
    }

    virtual const uint8_t*
    GetRawVectors();

 protected:
    virtual void
    QueryImpl(int64_t n, const uint8_t* data, int64_t k, float* distances, int64_t* labels, const Config& config);
};
```