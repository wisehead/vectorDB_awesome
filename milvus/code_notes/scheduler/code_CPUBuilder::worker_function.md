#1.CPUBuilder::worker_function

```
CPUBuilder::worker_function
--while (running_) 
----auto task = queue_.front();
----queue_.pop();
----task->Load(LoadType::DISK2CPU, 0);
------XBuildIndexTask::Load
----task->Execute();
------XBuildIndexTask::Execute
```