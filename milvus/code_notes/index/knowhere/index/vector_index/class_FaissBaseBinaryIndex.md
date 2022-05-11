#1.class FaissBaseBinaryIndex

```cpp
class FaissBaseBinaryIndex {
 protected:
    explicit FaissBaseBinaryIndex(std::shared_ptr<faiss::IndexBinary> index) : index_(std::move(index)) {
    }

    virtual BinarySet
    SerializeImpl(const IndexType& type);

    virtual void
    LoadImpl(const BinarySet& index_binary, const IndexType& type);

 public:
    std::shared_ptr<faiss::IndexBinary> index_ = nullptr;
};

```