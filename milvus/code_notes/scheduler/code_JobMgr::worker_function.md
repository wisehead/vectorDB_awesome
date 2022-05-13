#1.JobMgr::worker_function

```
JobMgr::worker_function
--while (running_)
----cv_.wait(lock, [this] { return !queue_.empty(); });
----auto job = queue_.front();
----queue_.pop();
----auto tasks = build_task(job);
------JobMgr::build_task
--------TaskCreator::Create
----auto search_job = std::dynamic_pointer_cast<SearchJob>(job);
----if (search_job != nullptr)
------
```