#1.ResourceMgr::RegisterSubscriber

```
ResourceMgr::RegisterSubscriber
--subscriber_ = std::move(subscriber);
```

#2.caller

```
Scheduler::Scheduler
--res_mgr_->RegisterSubscriber(std::bind(&Scheduler::PostEvent, this, std::placeholders::_1));
```

#3.Scheduler::PostEvent

```
Scheduler::PostEvent
--{
        std::lock_guard<std::mutex> lock(event_mutex_);
        event_queue_.push(event);
--}
--event_cv_.notify_one();
```

#4.Scheduler::worker_function

```
Scheduler::worker_function
--while (running_)
----std::unique_lock<std::mutex> lock(event_mutex_);
----event_cv_.wait(lock, [this] { return !event_queue_.empty(); });
----auto event = event_queue_.front();
----event_queue_.pop();
----process(event);
```