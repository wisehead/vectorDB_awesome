#1.CpuCacheMgr::GetIndex

```
CpuCacheMgr::GetIndex
--CacheMgr<ItemObj>::GetItem
----cache_->get(key);
------Cache<ItemObj>::get
--------lru_.get(key);
----------LRU.get
------------auto it = cache_items_map_.find(key);
```