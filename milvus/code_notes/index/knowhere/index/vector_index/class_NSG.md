#1.class NSG

```cpp
class NSG : public VecIndex {
 public:
    explicit NSG(const int64_t gpu_num = -1) : gpu_(gpu_num) {
        if (gpu_ >= 0) {
            index_mode_ = IndexMode::MODE_GPU;
        }
        index_type_ = IndexEnum::INDEX_NSG;
    }

    BinarySet
    Serialize(const Config& config = Config()) override;

    void
    Load(const BinarySet&) override;

    void
    BuildAll(const DatasetPtr&, const Config&) override;

    void
    Train(const DatasetPtr&, const Config&) override {
        KNOWHERE_THROW_MSG("NSG not support build item dynamically, please invoke BuildAll interface.");
    }

    void
    AddWithoutIds(const DatasetPtr&, const Config&) override {
        KNOWHERE_THROW_MSG("Incremental index NSG is not supported");
    }

    DatasetPtr
    Query(const DatasetPtr&, const Config&) override;

    int64_t
    Count() override;

    int64_t
    Dim() override;

    void
    UpdateIndexSize() override;

 private:
    int64_t gpu_;
    std::shared_ptr<impl::NsgIndex> index_;
};
```