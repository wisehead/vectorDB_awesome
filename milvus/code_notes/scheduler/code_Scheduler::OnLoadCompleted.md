#1.Scheduler::OnLoadCompleted

```
Scheduler::OnLoadCompleted
--auto load_completed_event = std::static_pointer_cast<LoadCompletedEvent>(event);
--auto resource = event->resource_;
--resource->WakeupExecutor();
----Resource::WakeupExecutor
--auto task_table_type = load_completed_event->task_table_item_->get_task()->label()->Type();
--switch (task_table_type) 
----case TaskLabelType::SPECIFIED_RESOURCE: 
------Action::SpecifiedResourceLabelTaskScheduler(res_mgr_, resource, load_completed_event);
----case TaskLabelType::BROADCAST: 
------if (resource->HasExecutor() == false) {
--------load_completed_event->task_table_item_->Move();
------Action::PushTaskToAllNeighbour(load_completed_event->task_table_item_, resource);
--resource->WakeupLoader();
```