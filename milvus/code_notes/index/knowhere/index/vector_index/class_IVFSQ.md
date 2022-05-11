#1.class IVFSQ

```cpp
class IVFSQ : public IVF {
 public:
    IVFSQ() : IVF() {
        index_type_ = IndexEnum::INDEX_FAISS_IVFSQ8;
    }

    explicit IVFSQ(std::shared_ptr<faiss::Index> index) : IVF(std::move(index)) {
        index_type_ = IndexEnum::INDEX_FAISS_IVFSQ8;
    }

    void
    Train(const DatasetPtr&, const Config&) override;

    VecIndexPtr
    CopyCpuToGpu(const int64_t, const Config&) override;

    void
    UpdateIndexSize() override;
};
```