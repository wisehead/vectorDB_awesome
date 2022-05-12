#1.ResourceMgr::post_event

```
ResourceMgr::post_event
--{                                                   
----std::lock_guard<std::mutex> lock(event_mutex_); 
----queue_.emplace(event);                          
--}                                                   
--event_cv_.notify_one();                             

```

#2.consumer/waiter ResourceMgr::event_process

```cpp
void
ResourceMgr::event_process() {
    SetThreadName("resevt_thread");
    while (running_) {
        std::unique_lock<std::mutex> lock(event_mutex_);
        event_cv_.wait(lock, [this] { return !queue_.empty(); });

        auto event = queue_.front();
        queue_.pop();
        lock.unlock();
        if (event == nullptr) {
            break;
        }

        if (subscriber_) {
            subscriber_(event);
        }
    }
}

```
