#1.MemManagerImpl::InsertEntitiesNoLock

```
MemManagerImpl::InsertEntitiesNoLock
--MemTablePtr mem = GetMemByTable(collection_id);
--mem->SetLSN(lsn);
--auto status = mem->AddEntities(source);
```