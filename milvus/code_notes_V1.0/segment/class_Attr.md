#1.class Attr

```cpp
class Attr {
 private:
    std::vector<uint8_t> data_;
    size_t nbytes_;
    std::vector<int64_t> uids_;
    std::string name_;
    std::string collection_id_;
};
```