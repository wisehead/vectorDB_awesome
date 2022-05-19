#1.TaskTable::Put

```
TaskTable::Put
--auto item = std::make_shared<TaskTableItem>(std::move(from));
--item->id = id_++;                                            
--item->set_task(std::move(task));                             
--item->state = TaskTableItemState::START;                     
--item->timestamp.start = get_current_timestamp();             
--table_.put(std::move(item));                                 
--if (subscriber_) {                                           
----subscriber_();                                                                                                  

```

#2.subscriber_ TaskTable::RegisterSubscriber

```cpp
inline void
    RegisterSubscriber(std::function<void(void)> subscriber) {
        subscriber_ = std::move(subscriber);
    }
```