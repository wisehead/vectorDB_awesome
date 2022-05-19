#1.code_Resource::WakeupExecutor

```
code_Resource::WakeupExecutor
--{
        std::lock_guard<std::mutex> lock(exec_mutex_);
        exec_flag_ = true;
--}
--exec_cv_.notify_one();
```

#2.waiter Resource::executor_function

```
Resource::executor_function
--while (running_) {
        std::unique_lock<std::mutex> lock(exec_mutex_);
        exec_cv_.wait(lock, [&] { return exec_flag_; });
        exec_flag_ = false;
        lock.unlock();
        while (true) {
            auto task_item = pick_task_execute();
```