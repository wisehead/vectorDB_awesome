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
--MXLogRecordHeader* head = (MXLogRecordHeader*)(current_read_buf + current_read_offset);
    record.type = (MXLogType)head->mxl_type;
    record.lsn = head->mxl_lsn;
    record.length = head->vector_num;
    record.data_size = head->data_size;
--current_read_offset += SizeOfMXLogRecordHeader;
--if (head->collection_id_size != 0) {
        record.collection_id.assign(current_read_buf + current_read_offset, head->collection_id_size);
        current_read_offset += head->collection_id_size;
    } else {
        record.collection_id = "";
    }
--if (head->partition_tag_size != 0) {
        record.partition_tag.assign(current_read_buf + current_read_offset, head->partition_tag_size);
        current_read_offset += head->partition_tag_size;
    } else {
        record.partition_tag = "";
    }
--if (head->vector_num != 0) {
        record.ids = (IDNumber*)(current_read_buf + current_read_offset);
        current_read_offset += head->vector_num * sizeof(IDNumber);
    } else {
        record.ids = nullptr;
    }

--if (record.data_size != 0) {
        record.data = current_read_buf + current_read_offset;
    } else {
        record.data = nullptr;
    }

--mxlog_buffer_reader_.buf_offset = uint32_t(head->mxl_lsn & LSN_OFFSET_MASK);    
```