#1.WalManager::GetNextRecord

```
WalManager::GetNextRecord
--

```


#2.lambda check_flush

```cpp
auto check_flush = [&]() -> bool {
--if (flush_info_.IsValid()) {
----if (p_buffer_->GetReadLsn() >= flush_info_.lsn_) {
------MXLogBuffer::GetReadLsn
--------BuildLsn(mxlog_buffer_reader_.file_no, mxlog_buffer_reader_.buf_offset, read_lsn);
------// can exec flush requirement
------record.type = MXLogType::Flush;
------record.collection_id = flush_info_.collection_id_;
------record.lsn = flush_info_.lsn_;
------flush_info_.Clear();
```