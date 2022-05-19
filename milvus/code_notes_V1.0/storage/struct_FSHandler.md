#1.struct FSHandler

```cpp
struct FSHandler {
    IOReaderPtr reader_ptr_ = nullptr;
    IOWriterPtr writer_ptr_ = nullptr;
    OperationPtr operation_ptr_ = nullptr;

    FSHandler(IOReaderPtr& reader_ptr, IOWriterPtr& writer_ptr, OperationPtr& operation_ptr)
        : reader_ptr_(reader_ptr), writer_ptr_(writer_ptr), operation_ptr_(operation_ptr) {
    }
};
```