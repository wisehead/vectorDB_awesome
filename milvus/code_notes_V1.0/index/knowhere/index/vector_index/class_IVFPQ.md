#1.class IVFPQ

```cpp
class IVFPQ : public IVF {
 public:
    IVFPQ() : IVF() {
        index_type_ = IndexEnum::INDEX_FAISS_IVFPQ;
    }

    explicit IVFPQ(std::shared_ptr<faiss::Index> index) : IVF(std::move(index)) {
        index_type_ = IndexEnum::INDEX_FAISS_IVFPQ;
    }

    void
    Train(const DatasetPtr&, const Config&) override;

    VecIndexPtr
    CopyCpuToGpu(const int64_t, const Config&) override;

    void
    UpdateIndexSize() override;

 protected:
    std::shared_ptr<faiss::IVFSearchParameters>
    GenParams(const Config& config) override;
};
```