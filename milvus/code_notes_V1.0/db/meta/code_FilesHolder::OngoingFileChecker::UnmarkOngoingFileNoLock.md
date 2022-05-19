#1.FilesHolder::OngoingFileChecker::UnmarkOngoingFileNoLock

```
FilesHolder::OngoingFileChecker::UnmarkOngoingFileNoLock
--auto iter = ongoing_files_.find(table_file.collection_id_);
--if (iter != ongoing_files_.end())
----auto it_file = iter->second.find(table_file.id_);
----if (it_file != iter->second.end())
------it_file->second--;
------if (it_file->second <= 0)
--------iter->second.erase(table_file.id_);
--------if (iter->second.empty()) {
----------ongoing_files_.erase(table_file.collection_id_);
```