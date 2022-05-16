#1.MemTable::Delete

```
MemTable::Delete
--for (auto& table_file : mem_table_file_list_) {
----table_file->Delete(doc_ids);
------MemTableFile::Delete

// Add the id to delete list so it can be applied to other segments on disk during the next flush
--for (auto& id : doc_ids) {
----doc_ids_to_delete_.insert(id);

```