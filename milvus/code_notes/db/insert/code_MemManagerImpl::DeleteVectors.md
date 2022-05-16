#1.MemManagerImpl::DeleteVectors

```
MemManagerImpl::DeleteVectors
--MemTablePtr mem = GetMemByTable(collection_id);
--mem->SetLSN(lsn);

--IDNumbers ids;
--ids.resize(length);
--memcpy(ids.data(), vector_ids, length * sizeof(IDNumber));

--auto status = mem->Delete(ids);
----MemTable::Delete
------
```