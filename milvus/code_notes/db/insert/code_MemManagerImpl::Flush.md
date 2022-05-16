#1.MemManagerImpl::Flush

```
MemManagerImpl::Flush
--ToImmutable(collection_id);
----MemManagerImpl::ToImmutable
--MemList temp_immutable_list;
  {
        std::unique_lock<std::mutex> lock(mutex_);
        immu_mem_list_.swap(temp_immutable_list);
  }
--auto max_lsn = GetMaxLSN(temp_immutable_list);
--for (auto& mem : temp_immutable_list) {
----auto status = mem->Serialize(max_lsn, true);
```