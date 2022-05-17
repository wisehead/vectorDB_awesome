#1.MXLogFileHandler::Load

```
MXLogFileHandler::Load
--if (OpenFile()) {
----MXLogFileHandler::OpenFile
----uint32_t file_size = GetFileSize();
----if (file_size > data_offset) {
            read_size = file_size - data_offset;
            fseek(p_file_, data_offset, SEEK_SET);
            auto ret = fread(buf, 1, read_size, p_file_);
            __glibcxx_assert(ret == read_size);
----}
--}
--return read_size;
```