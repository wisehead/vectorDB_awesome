#1.WalManager::CreateCollection

```
WalManager::CreateCollection
--uint64_t applied_lsn = last_applied_lsn_;
--collections_[collection_id][""] = {applied_lsn, applied_lsn};
--return applied_lsn;
}
```