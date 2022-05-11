#1.class FaissBaseIndex

```cpp
class FaissBaseIndex {
 protected:
    explicit FaissBaseIndex(std::shared_ptr<faiss::Index> index) : index_(std::move(index)) {
    }

    virtual BinarySet
    SerializeImpl(const IndexType& type);

    virtual void
    LoadImpl(const BinarySet&, const IndexType& type);

    virtual void
    SealImpl() { /* do nothing */
    }

 public:
    std::shared_ptr<faiss::Index> index_ = nullptr;
};

```