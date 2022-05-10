#1.class VecIndex

```cpp
class VecIndex : public Index {

 protected:
    IndexType index_type_ = "";
    IndexMode index_mode_ = IndexMode::MODE_CPU;
    std::shared_ptr<std::vector<IDType>> uids_ = nullptr;
    int64_t index_size_ = -1;

 private:
    // multi thread may access bitset_
    std::mutex bitset_mutex_;
    faiss::ConcurrentBitsetPtr bitset_ = nullptr;
};

```