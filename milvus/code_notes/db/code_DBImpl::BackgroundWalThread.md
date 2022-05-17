#1.DBImpl::BackgroundWalThread(

```
DBImpl::BackgroundWalThread
--server::SystemInfo::GetInstance().Init();
--InternalFlush();
--while (true)
----if (options_.auto_flush_interval_ > 0) {
------if (std::chrono::system_clock::now() >= next_auto_flush_time) {
--------InternalFlush();
--------next_auto_flush_time = get_next_auto_flush_time();
----wal_mgr_->GetNextRecord(record);
```