#1.class Operation

```cpp
class Operation {
 public:
    virtual void
    CreateDirectory() = 0;

    virtual const std::string&
    GetDirectory() const = 0;

    virtual void
    ListDirectory(std::vector<std::string>& file_paths) = 0;

    virtual bool
    DeleteFile(const std::string& file_path) = 0;

    // TODO(zhiru):
    //  open(), sync(), close()
    //  function that opens a stream for reading file
    //  function that creates a new, empty file and returns an stream for appending data to this file
    //  function that creates a new, empty, temporary file and returns an stream for appending data to this file
};

```