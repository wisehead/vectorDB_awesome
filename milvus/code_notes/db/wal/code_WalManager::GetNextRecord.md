#1.WalManager::GetNextRecord

```
WalManager::GetNextRecord
--if (check_flush()) {
        return WAL_SUCCESS;
--}
--while (WAL_SUCCESS == p_buffer_->Next(last_applied_lsn_, record))
----if (record.type == MXLogType::None)
------if (check_flush())
--------return WAL_SUCCESS;
------break;
----auto it_col = collections_.find(record.collection_id);
----if (it_col != collections_.end()) {
------auto it_part = it_col->second.find(record.partition_tag);
------if (it_part->second.flush_lsn < record.lsn) {
--------break;

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