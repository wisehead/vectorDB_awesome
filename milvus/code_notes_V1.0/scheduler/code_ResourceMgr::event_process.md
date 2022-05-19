#1.ResourceMgr::event_process

```
ResourceMgr::event_process
--while (running_)
----std::unique_lock<std::mutex> lock(event_mutex_);
----event_cv_.wait(lock, [this] { return !queue_.empty(); });
----auto event = queue_.front();
----queue_.pop();
----lock.unlock();
----if (subscriber_) {
------subscriber_(event);
```