#1.class SearchReqStrategy

```cpp
class SearchReqStrategy : public RequestStrategy, public EngineConfigHandler {
 public:
    SearchReqStrategy();

    Status
    ReScheduleQueue(const BaseRequestPtr& request, std::queue<BaseRequestPtr>& queue) override;
};
```