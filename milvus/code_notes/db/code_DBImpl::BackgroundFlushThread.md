#1.DBImpl::BackgroundFlushThread

```
DBImpl::BackgroundFlushThread
--while (true) {
----if (!initialized_.load(std::memory_order_acquire)) {
            LOG_ENGINE_DEBUG_ << "DB background flush thread exit";
            break;
----}

----InternalFlush();
----if (options_.auto_flush_interval_ > 0) {
            swn_flush_.Wait_For(std::chrono::seconds(options_.auto_flush_interval_));
----} else {
            swn_flush_.Wait();//caller is DBImpl::Stop, let it die
----}
--}
```