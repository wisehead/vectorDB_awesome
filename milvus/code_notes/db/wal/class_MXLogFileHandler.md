#1.struct MXLogFileHandler

```cpp
class MXLogFileHandler {

 private:
    std::string file_path_;
    std::string file_name_;
    std::string file_mode_;
    FILE* p_file_;
};
 
```