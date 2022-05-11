#1.class BinarySet

```cpp
class BinarySet {
 public:
    BinaryPtr
    GetByName(const std::string& name) const {
        return binary_map_.at(name);
    }

    void
    Append(const std::string& name, BinaryPtr binary) {
        binary_map_[name] = std::move(binary);
    }

    void
    Append(const std::string& name, std::shared_ptr<uint8_t[]> data, int64_t size) {
        auto binary = std::make_shared<Binary>();
        binary->data = data;
        binary->size = size;
        binary_map_[name] = std::move(binary);
    }

    // void
    // Append(const std::string &name, void *data, int64_t size, ID id) {
    //    Binary binary;
    //    binary.data = data;
    //    binary.size = size;
    //    binary.id = id;
    //    binary_map_[name] = binary;
    //}

    void
    clear() {
        binary_map_.clear();
    }

 public:
    std::map<std::string, BinaryPtr> binary_map_;
};

```