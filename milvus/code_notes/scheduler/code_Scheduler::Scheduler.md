#1.Scheduler::Scheduler

```
Scheduler::Scheduler
--res_mgr_->RegisterSubscriber(std::bind(&Scheduler::PostEvent, this, std::placeholders::_1));
--event_register_.insert(std::make_pair(static_cast<uint64_t>(EventType::START_UP),
                                          std::bind(&Scheduler::OnStartUp, this, std::placeholders::_1)));
--event_register_.insert(std::make_pair(static_cast<uint64_t>(EventType::LOAD_COMPLETED),
                                          std::bind(&Scheduler::OnLoadCompleted, this, std::placeholders::_1)));
--event_register_.insert(std::make_pair(static_cast<uint64_t>(EventType::TASK_TABLE_UPDATED),
                                          std::bind(&Scheduler::OnTaskTableUpdated, this, std::placeholders::_1)));
--event_register_.insert(std::make_pair(static_cast<uint64_t>(EventType::FINISH_TASK),
                                          std::bind(&Scheduler::OnFinishTask, this, std::placeholders::_1)));
```