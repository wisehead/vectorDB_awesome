#1.Scheduler::process

```
Scheduler::process
--auto process_event = event_register_.at(static_cast<int>(event->Type()));
--process_event(event);
```

#2.Scheduler::OnStartUp

```
Scheduler::OnStartUp
--event->resource_->WakeupLoader();
```

#3.Scheduler::OnFinishTask

```
Scheduler::OnFinishTask
--event->resource_->WakeupLoader();
```

#4.Scheduler::OnTaskTableUpdated

```
Scheduler::OnTaskTableUpdated
--event->resource_->WakeupLoader();
```

#5.Scheduler::OnLoadCompleted

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
```