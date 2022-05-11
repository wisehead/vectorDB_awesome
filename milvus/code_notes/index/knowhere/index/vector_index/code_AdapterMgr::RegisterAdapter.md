#1.AdapterMgr::RegisterAdapter

```cpp
#define REGISTER_CONF_ADAPTER(T, TYPE, NAME) static AdapterMgr::register_t<T> reg_##NAME##_(TYPE)

void
AdapterMgr::RegisterAdapter() {
    init_ = true;

    REGISTER_CONF_ADAPTER(ConfAdapter, IndexEnum::INDEX_FAISS_IDMAP, idmap_adapter);
    REGISTER_CONF_ADAPTER(IVFConfAdapter, IndexEnum::INDEX_FAISS_IVFFLAT, ivf_adapter);
    REGISTER_CONF_ADAPTER(IVFPQConfAdapter, IndexEnum::INDEX_FAISS_IVFPQ, ivfpq_adapter);
    REGISTER_CONF_ADAPTER(IVFSQConfAdapter, IndexEnum::INDEX_FAISS_IVFSQ8, ivfsq8_adapter);
    REGISTER_CONF_ADAPTER(IVFSQConfAdapter, IndexEnum::INDEX_FAISS_IVFSQ8H, ivfsq8h_adapter);
    REGISTER_CONF_ADAPTER(BinIDMAPConfAdapter, IndexEnum::INDEX_FAISS_BIN_IDMAP, idmap_bin_adapter);
    REGISTER_CONF_ADAPTER(BinIVFConfAdapter, IndexEnum::INDEX_FAISS_BIN_IVFFLAT, ivf_bin_adapter);
    REGISTER_CONF_ADAPTER(NSGConfAdapter, IndexEnum::INDEX_NSG, nsg_adapter);
    REGISTER_CONF_ADAPTER(ConfAdapter, IndexEnum::INDEX_SPTAG_KDT_RNT, sptag_kdt_adapter);
    REGISTER_CONF_ADAPTER(ConfAdapter, IndexEnum::INDEX_SPTAG_BKT_RNT, sptag_bkt_adapter);
    REGISTER_CONF_ADAPTER(HNSWConfAdapter, IndexEnum::INDEX_HNSW, hnsw_adapter);
    REGISTER_CONF_ADAPTER(ANNOYConfAdapter, IndexEnum::INDEX_ANNOY, annoy_adapter);
}
```