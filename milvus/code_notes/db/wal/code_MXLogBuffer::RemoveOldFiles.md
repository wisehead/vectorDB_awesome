#1.MXLogBuffer::RemoveOldFiles

```
MXLogBuffer::RemoveOldFiles
--ParserLsn(flushed_lsn, file_no, offset);
--if (file_no_from_ < file_no) 
----MXLogFileHandler file_handler(mxlog_writer_.GetFilePath());
----do {
------file_handler.SetFileName(ToFileName(file_no_from_));
------file_handler.DeleteFile();
----} while (++file_no_from_ < file_no);
```