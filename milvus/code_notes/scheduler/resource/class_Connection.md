#1.class Connection

```cpp
class Connection {
 public:
    // TODO: update construct function, speed: double->uint64_t
    Connection(std::string name, double speed) : name_(std::move(name)), speed_(speed) {
    }

    const std::string&
    name() const {
        return name_;
    }

    uint64_t
    speed() const {
        return speed_;
    }

    uint64_t
    transport_cost() {
        return 1024 / speed_;
    }

 public:
    std::string
    Dump() const {
        std::stringstream ss;
        ss << "<name: " << name_ << ", speed: " << speed_ << ">";
        return ss.str();
    }

 private:
    std::string name_;
    uint64_t speed_;
};
```