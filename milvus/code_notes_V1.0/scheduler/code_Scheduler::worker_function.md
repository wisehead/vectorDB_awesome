#1.Scheduler::worker_function

```
Scheduler::worker_function
--while (running_) {
        std::unique_lock<std::mutex> lock(event_mutex_);
        event_cv_.wait(lock, [this] { return !event_queue_.empty(); });
        auto event = event_queue_.front();
        event_queue_.pop();
        if (event == nullptr) {
            break;
        }

        process(event);
        --Scheduler::process
    }
```