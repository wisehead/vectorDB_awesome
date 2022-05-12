#1.Action::SpecifiedResourceLabelTaskScheduler

```
Action::SpecifiedResourceLabelTaskScheduler
--auto task_item = event->task_table_item_;
--auto task = event->task_table_item_->get_task();
--if (resource->name() == task->path().Last()) {
        resource->WakeupExecutor();
--}
--else
----auto next_res_name = task->path().Next();
----auto next_res = res_mgr->GetResource(next_res_name);
----event->task_table_item_->Move();
----next_res->task_table().Put(task, task_item);
```