#1.CommonUtil::EraseFromCache

```
CommonUtil::EraseFromCache
--cache::CpuCacheMgr::GetInstance()->EraseItem(item_key);
----CacheMgr<ItemObj>::EraseItem
------cache_->erase(key);
--------Cache<ItemObj>::erase
----------erase_internal(key);
------------Cache<ItemObj>::erase_internal
--------------lru_.erase(key);
----------------LRU::erase
------------------auto it = cache_items_map_.find(key);
--------------------if (it != cache_items_map_.end()) {
----------------------cache_items_list_.erase(it->second);
----------------------cache_items_map_.erase(it);

```