#1.Resource::pick_task_execute

```
Resource::pick_task_execute
--auto indexes = task_table_.PickToExecute(std::numeric_limits<uint64_t>::max());
--for (auto index : indexes)
----if (task_table_[index]->get_task()->label()->Type() == TaskLabelType::SPECIFIED_RESOURCE) {
------if (task_table_[index]->get_task()->path().Last() != name()) 
--------continue
----task_table_.Execute(index)
------TaskTable::Execute
--------table_[index]->Execute();
----------TaskTableItem::Execute
------------if (state == TaskTableItemState::LOADED) {
--------------state = TaskTableItemState::EXECUTING;
--return task_table_.at(index);
```