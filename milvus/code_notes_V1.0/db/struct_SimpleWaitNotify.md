#1.struct SimpleWaitNotify

```cpp
    struct SimpleWaitNotify {
        bool notified_ = false;
        std::mutex mutex_;
        std::condition_variable cv_;

        void
        Wait() {
            std::unique_lock<std::mutex> lck(mutex_);
            if (!notified_) {
                cv_.wait(lck);
            }
            notified_ = false;
        }

        std::cv_status
        Wait_Until(const std::chrono::system_clock::time_point& tm_pint) {
            std::unique_lock<std::mutex> lck(mutex_);
            std::cv_status ret = std::cv_status::timeout;
            if (!notified_) {
                ret = cv_.wait_until(lck, tm_pint);
            }
            notified_ = false;
            return ret;
        }

        std::cv_status
        Wait_For(const std::chrono::system_clock::duration& tm_dur) {
            std::unique_lock<std::mutex> lck(mutex_);
            std::cv_status ret = std::cv_status::timeout;
            if (!notified_) {
                ret = cv_.wait_for(lck, tm_dur);
            }
            notified_ = false;
            return ret;
        }

        void
        Notify() {
            std::unique_lock<std::mutex> lck(mutex_);
            notified_ = true;
            lck.unlock();
            cv_.notify_one();
        }
    };
```