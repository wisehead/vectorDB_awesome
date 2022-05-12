#1.enum EngineType

```cpp
enum class EngineType {
    INVALID = 0,
    FAISS_IDMAP = 1,
    FAISS_IVFFLAT,
    FAISS_IVFSQ8,
    NSG_MIX,
    FAISS_IVFSQ8H,
    FAISS_PQ,
    SPTAG_KDT,
    SPTAG_BKT,
    FAISS_BIN_IDMAP,
    FAISS_BIN_IVFFLAT,
    HNSW,
    ANNOY,
    MAX_VALUE = ANNOY,
};
```