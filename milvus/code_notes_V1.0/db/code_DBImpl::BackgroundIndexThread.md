#1.DBImpl::BackgroundIndexThread

```
DBImpl::BackgroundIndexThread
--while (true) {
        if (!initialized_.load(std::memory_order_acquire)) {
            WaitMergeFileFinish();
            WaitBuildIndexFinish();

            LOG_ENGINE_DEBUG_ << "DB background thread exit";
            break;
        }

        swn_index_.Wait_For(std::chrono::seconds(BACKGROUND_INDEX_INTERVAL));//caller is DBImpl::Stop

        WaitMergeFileFinish();
        StartBuildIndexTask();
--}
```