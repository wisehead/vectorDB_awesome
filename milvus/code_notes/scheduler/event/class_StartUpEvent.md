#1.class StartUpEvent

```
class StartUpEvent : public Event {
 public:
    explicit StartUpEvent(std::shared_ptr<Resource> resource) : Event(EventType::START_UP, std::move(resource)) {
    }

    inline std::string
    Dump() const override {
        return "<StartUpEvent>";
    }

    friend std::ostream&
    operator<<(std::ostream& out, const StartUpEvent& event);
};
```