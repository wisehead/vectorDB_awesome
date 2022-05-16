#1.MemTable::Serialize

```
MemTable::Serialize
--if (!doc_ids_to_delete_.empty() && apply_delete) {
----auto status = ApplyDeletes();
--for (auto mem_table_file = mem_table_file_list_.begin(); mem_table_file != mem_table_file_list_.end();) {
----auto status = (*mem_table_file)->Serialize(wal_lsn);
------MemTableFile::Serialize
----update_files.push_back((*mem_table_file)->GetSegmentSchema());
----mem_table_file = mem_table_file_list_.erase(mem_table_file);
```