#1.class ConnectionContext

```cpp
class ConnectionContext {
 public:
    virtual ~ConnectionContext() {
    }
    virtual bool
    IsConnectionBroken() const = 0;
};
```