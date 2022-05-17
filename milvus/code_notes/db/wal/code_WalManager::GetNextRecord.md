#1.WalManager::GetNextRecord

```
WalManager::GetNextRecord
--

```


#2.lambda check_flush

```cpp
auto check_flush = [&]() -> bool {
        std::lock_guard<std::mutex> lck(mutex_);
        if (flush_info_.IsValid()) {
            if (p_buffer_->GetReadLsn() >= flush_info_.lsn_) {
                // can exec flush requirement
                record.type = MXLogType::Flush;
                record.collection_id = flush_info_.collection_id_;
                record.lsn = flush_info_.lsn_;
                flush_info_.Clear();

                LOG_WAL_INFO_ << "record flush collection " << record.collection_id << " lsn " << record.lsn;
                return true;
            }
        }
        return false;
    };


```