#1.class MXLogBuffer

```cpp
class MXLogBuffer {

 private:
    uint32_t mxlog_buffer_size_;  // from config
    BufferPtr buf_[2];
    std::mutex mutex_;
    uint32_t file_no_from_;
    MXLogBufferHandler mxlog_buffer_reader_;
    MXLogBufferHandler mxlog_buffer_writer_;
    MXLogFileHandler mxlog_writer_;
};
```