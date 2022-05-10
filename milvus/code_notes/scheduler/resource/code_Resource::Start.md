#1.Resource::Start

```
Resource::Start
--running_ = true;
--loader_thread_ = std::thread(&Resource::loader_function, this);
--executor_thread_ = std::thread(&Resource::executor_function, this);
```

#2.Resource::loader_function

```
Resource::loader_function
--while (running_)
----std::unique_lock<std::mutex> lock(load_mutex_);
    load_cv_.wait(lock, [&] { return load_flag_; });
    load_flag_ = false;
    lock.unlock();
----while (true)    
------auto task_item = pick_task_load();
------if (task_item->get_task()->Type() == TaskType::BuildIndexTask && name() == "cpu")
--------BuildMgrInst::GetInstance()->Take();
```

#3.Resource::pick_task_load

```
Resource::pick_task_load
--auto indexes = task_table_.PickToLoad(10);
--for (auto index : indexes) {
----// try to set one task loading, then return
----if (task_table_.Load(index)) 
--------table_[index]->Load()
----------TaskTableItem::Load
------return task_table_.at(index);
        // else try next
```

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