#1.Resource::executor_function

```
Resource::executor_function
--if (subscriber_) {
----auto event = std::make_shared<StartUpEvent>(shared_from_this());
----subscriber_(std::static_pointer_cast<Event>(event));
--while (running_) 
----while (true)
------Process(task_item->get_task());
--------CpuResource::Process
----------XBuildIndexTask::Execute
------task_item->set_task(std::move(FinishedTask::Create(task_item->get_task())));
------++total_task_;
------total_cost_ += finish - start;
------task_item->Executed();
--------state = TaskTableItemState::EXECUTED;
------if (task_item->get_task()->Type() == TaskType::BuildIndexTask) {
--------BuildMgrInst::GetInstance()->Put();
----------BuildMgr::Put
------------++available_;
--------ResMgrInst::GetInstance()->GetResource("cpu")->WakeupLoader();
----------Resource::WakeupLoader
------------load_flag_ = true;
------------load_cv_.notify_one();
--------ResMgrInst::GetInstance()->GetResource("disk")->WakeupLoader();
----------Resource::WakeupExecutor
------------exec_flag_ = true;
------------exec_cv_.notify_one();
------if (subscriber_) {
                auto event = std::make_shared<FinishTaskEvent>(shared_from_this(), task_item);
                subscriber_(std::static_pointer_cast<Event>(event));
            }
```