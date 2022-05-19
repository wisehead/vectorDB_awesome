#1.MemTableFile::AddEntities

```
MemTableFile::AddEntities
--size_t single_entity_mem_size = source->SingleEntitySize(table_file_schema_.dimension_);
--size_t mem_left = GetMemLeft();
--if (mem_left >= single_entity_mem_size)
----size_t num_entities_to_add = std::ceil(mem_left / single_entity_mem_size);
----source->AddEntities(segment_writer_ptr_, table_file_schema_, num_entities_to_add, num_entities_added);
----current_mem_ += (num_entities_added * single_entity_mem_size);
```