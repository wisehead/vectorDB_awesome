#1.class Event

```cpp
class Event {
 public:
    explicit Event(EventType type, std::shared_ptr<Resource> resource) : type_(type), resource_(std::move(resource)) {
    }

    inline EventType
    Type() const {
        return type_;
    }

    virtual std::string
    Dump() const = 0;

    friend std::ostream&
    operator<<(std::ostream& out, const Event& event);

 public:
    EventType type_;
    std::shared_ptr<Resource> resource_;
};

```