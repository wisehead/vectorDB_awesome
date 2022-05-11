#1.class IDMAP

```cpp
class IDMAP : public VecIndex, public FaissBaseIndex {
 public:
    IDMAP() : FaissBaseIndex(nullptr) {
        index_type_ = IndexEnum::INDEX_FAISS_IDMAP;
    }

    explicit IDMAP(std::shared_ptr<faiss::Index> index) : FaissBaseIndex(std::move(index)) {
        index_type_ = IndexEnum::INDEX_FAISS_IDMAP;
    }

    BinarySet
    Serialize(const Config& config = Config()) override;

    void
    Load(const BinarySet&) override;

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
        return Count() * Dim() * sizeof(FloatType);
    }

    VecIndexPtr
    CopyCpuToGpu(const int64_t, const Config&);

    virtual const float*
    GetRawVectors();

 protected:
    virtual void
    QueryImpl(int64_t, const float*, int64_t, float*, int64_t*, const Config&);
};
```