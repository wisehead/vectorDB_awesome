#1.MemManagerImpl::ToImmutable

```
MemManagerImpl::ToImmutable
--auto memIt = mem_id_map_.find(collection_id);
--if (memIt != mem_id_map_.end()) {
----if (!memIt->second->Empty()) {
------immu_mem_list_.push_back(memIt->second);
------mem_id_map_.erase(memIt);

```