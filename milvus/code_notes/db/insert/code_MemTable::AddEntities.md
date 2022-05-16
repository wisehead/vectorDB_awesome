#1.MemTable::AddEntities

```
MemTable::AddEntities
--while (!source->AllAdded())
----MemTableFilePtr current_mem_table_file;
----if (!mem_table_file_list_.empty()) {
------current_mem_table_file = mem_table_file_list_.back();
----if (mem_table_file_list_.empty() || current_mem_table_file->IsFull())
------MemTableFilePtr new_mem_table_file = std::make_shared<MemTableFile>(collection_id_, meta_, options_);
------status = new_mem_table_file->AddEntities(source);
------mem_table_file_list_.emplace_back(new_mem_table_file);
----else
------status = current_mem_table_file->AddEntities(source);
```