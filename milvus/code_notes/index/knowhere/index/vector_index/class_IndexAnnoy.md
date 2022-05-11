#1.class IndexAnnoy

```cpp
class IndexAnnoy : public VecIndex {
 public:
    IndexAnnoy() {
        index_type_ = IndexEnum::INDEX_ANNOY;
    }

    BinarySet
    Serialize(const Config& config = Config()) override;

    void
    Load(const BinarySet& index_binary) override;

    void
    BuildAll(const DatasetPtr& dataset_ptr, const Config& config) override;

    void
    Train(const DatasetPtr& dataset_ptr, const Config& config) override {
        KNOWHERE_THROW_MSG("Annoy not support build item dynamically, please invoke BuildAll interface.");
    }

    void
    AddWithoutIds(const DatasetPtr&, const Config&) override {
        KNOWHERE_THROW_MSG("Incremental index is not supported");
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
    MetricType metric_type_;
    std::shared_ptr<AnnoyIndexInterface<int64_t, float>> index_ = nullptr;
};

```