#1.class CPUSPTAGRNG

```cpp
class CPUSPTAGRNG : public VecIndex {
 public:
    explicit CPUSPTAGRNG(const std::string& IndexType);

 public:
    BinarySet
    Serialize(const Config& config = Config()) override;

    void
    Load(const BinarySet& index_array) override;

    void
    BuildAll(const DatasetPtr&, const Config&) override;

    void
    Train(const DatasetPtr& dataset_ptr, const Config& config) override {
        KNOWHERE_THROW_MSG("SPTAGRNG not support build item dynamically, please invoke BuildAll interface.");
    }

    void
    AddWithoutIds(const DatasetPtr&, const Config&) override {
        KNOWHERE_THROW_MSG("Incremental index SPTAGRNG is not supported");
    }

    DatasetPtr
    Query(const DatasetPtr& dataset_ptr, const Config& config) override;

    int64_t
    Count() override;

    int64_t
    Dim() override;

    void
    UpdateIndexSize() override;

 private:
    void
    SetParameters(const Config& config);

 private:
    std::shared_ptr<SPTAG::VectorIndex> index_ptr_;
};

```