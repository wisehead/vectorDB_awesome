#1.Resource::loader_function

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
------LoadFile(task_item->get_task());
--------CpuResource::LoadFile
----------task->Load(LoadType::DISK2CPU, 0);
------------XBuildIndexTask::Load//or other task
------task_item->Loaded();
--------TaskTableItem::Loaded
----------if (state == TaskTableItemState::LOADING) 
------------state = TaskTableItemState::LOADED;
------label = task_item->get_task()->label();
------if (task_item->from)
--------task_item->from->Moved();
----------TaskTableItem::Moved
------------if (state == TaskTableItemState::MOVING)
--------------state = TaskTableItemState::MOVED;
--------task_item->from->set_task(std::move(FinishedTask::Create(task_item->from->get_task())));
----------FinishedTask::Create
--------task_item->from = nullptr;
------if (subscriber_)
--------auto event = std::make_shared<LoadCompletedEvent>(shared_from_this(), task_item);
--------subscriber_(std::static_pointer_cast<Event>(event));
```

#2.Resource::pick_task_load

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

