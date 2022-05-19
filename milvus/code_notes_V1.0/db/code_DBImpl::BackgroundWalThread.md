#1.DBImpl::BackgroundWalThread

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
----if (record.type != wal::MXLogType::None) 
------ExecWalRecord(record);
------if (record.type == wal::MXLogType::Flush)
--------// notify flush request to return
--------flush_req_swn_.Notify();//waiter is DBImpl::Flush
----else
------if (!initialized_.load(std::memory_order_acquire)) {//准备shutdown
--------InternalFlush();
--------flush_req_swn_.Notify();
--------WaitMergeFileFinish();
----------DBImpl::WaitMergeFileFinish
------------for (auto& iter : merge_thread_results_) {
--------------iter.wait();
--------WaitBuildIndexFinish();
----------DBImpl::WaitBuildIndexFinish
------------for (auto& iter : index_thread_results_) {
--------------iter.wait();
--------break;
------}

------if (options_.auto_flush_interval_ > 0) {
--------swn_wal_.Wait_Until(next_auto_flush_time);
------} else {
--------swn_wal_.Wait();//caller is IUD operations, like insertVector/deleteVector

```