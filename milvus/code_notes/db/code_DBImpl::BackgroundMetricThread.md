#1.DBImpl::BackgroundMetricThread

```
DBImpl::BackgroundMetricThread
--while (true) {
        if (!initialized_.load(std::memory_order_acquire)) {
            LOG_ENGINE_DEBUG_ << "DB background metric thread exit";
            break;
        }

----swn_metric_.Wait_For(std::chrono::seconds(BACKGROUND_METRIC_INTERVAL));//call is DBImpl::Stop
----StartMetricTask();
----meta::FilesHolder::PrintInfo();
------FilesHolder::PrintInfo
--------OngoingFileChecker::GetInstance().PrintInfo();
----------FilesHolder::OngoingFileChecker::PrintInfo
------------for (meta::Table2FileRef::iterator iter = ongoing_files_.begin(); iter != ongoing_files_.end(); ++iter) {
--------------LOG_ENGINE_DEBUG_ << "\t" << iter->first << ": " << iter->second.size() << " files in use";
--}
```