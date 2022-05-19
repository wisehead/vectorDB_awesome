#4.TaskTable::PickToLoad

```
TaskTable::PickToLoad
--for (uint64_t i = 0, loaded_count = 0, pick_count = 0; i < table_.size() && pick_count < limit; ++i)
----if (not cross && table_[index]->IsFinish()) {
------table_.set_front(index);
----else if (table_[index]->state == TaskTableItemState::LOADED)
------cross = true;
      ++loaded_count;
      if (loaded_count >= 1)
        return std::vector<uint64_t>();
----else if (table_[index]->state == TaskTableItemState::START)
------auto task = table_[index]->get_task();
      cross = true;
      indexes.push_back(index);
      ++pick_count;     
--return indexes;         
```