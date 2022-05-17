#1.class RequestQueue

```cpp
class RequestQueue : public BlockingRequestQueue {
 public:
    RequestQueue();
    virtual ~RequestQueue();

    BaseRequestPtr
    TakeRequest();

    Status
    PutRequest(const BaseRequestPtr& request_ptr);
};
```