#1.VecIndexFactory::CreateVecIndex

```cpp
VecIndexFactory::CreateVecIndex() {
    if (type == IndexEnum::INDEX_FAISS_IDMAP) {
        return std::make_shared<knowhere::IDMAP>();
    } else if (type == IndexEnum::INDEX_FAISS_IVFFLAT) {
        return std::make_shared<knowhere::IVF>();
    } else if (type == IndexEnum::INDEX_FAISS_IVFPQ) {
        return std::make_shared<knowhere::IVFPQ>();
    } else if (type == IndexEnum::INDEX_FAISS_IVFSQ8) {
        return std::make_shared<knowhere::IVFSQ>();
    } else if (type == IndexEnum::INDEX_FAISS_BIN_IDMAP) {
        return std::make_shared<knowhere::BinaryIDMAP>();
    } else if (type == IndexEnum::INDEX_FAISS_BIN_IVFFLAT) {
        return std::make_shared<knowhere::BinaryIVF>();
    } else if (type == IndexEnum::INDEX_NSG) {
        return std::make_shared<knowhere::NSG>(-1);
    } else if (type == IndexEnum::INDEX_SPTAG_KDT_RNT) {
        return std::make_shared<knowhere::CPUSPTAGRNG>("KDT");
    } else if (type == IndexEnum::INDEX_SPTAG_BKT_RNT) {
        return std::make_shared<knowhere::CPUSPTAGRNG>("BKT");
    } else if (type == IndexEnum::INDEX_HNSW) {
        return std::make_shared<knowhere::IndexHNSW>();
    } else if (type == IndexEnum::INDEX_ANNOY) {
        return std::make_shared<knowhere::IndexAnnoy>();
    } else {
        return nullptr;
    }
}
```