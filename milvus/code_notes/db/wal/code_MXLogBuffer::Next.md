#1.MXLogBuffer::Next

```
MXLogBuffer::Next
--// reader catch up to writer, no next record, read fail
--if (GetReadLsn() >= last_applied_lsn) {
----return WAL_SUCCESS;
--if (mxlog_buffer_reader_.file_no != mxlog_buffer_writer_.file_no) {
        if (mxlog_buffer_reader_.buf_offset == mxlog_buffer_reader_.max_offset) {  // last record
            mxlog_buffer_reader_.file_no++;
            mxlog_buffer_reader_.buf_offset = 0;
            need_load_new = (mxlog_buffer_reader_.file_no != mxlog_buffer_writer_.file_no);
            if (!need_load_new) {
                // read reach write buffer
                mxlog_buffer_reader_.buf_idx = mxlog_buffer_writer_.buf_idx;
            }
        }
--}
--if (need_load_new) {
----MXLogFileHandler mxlog_reader(mxlog_writer_.GetFilePath());
----mxlog_reader.SetFileName(ToFileName(mxlog_buffer_reader_.file_no));
----mxlog_reader.SetFileOpenMode("r");
----uint32_t file_size = mxlog_reader.Load(buf_[mxlog_buffer_reader_.buf_idx].get(), 0);
------MXLogFileHandler::Load
----mxlog_buffer_reader_.max_offset = file_size;
--}
```