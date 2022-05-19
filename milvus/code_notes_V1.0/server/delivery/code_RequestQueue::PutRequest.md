#1.RequestQueue::PutRequest

```
RequestQueue::PutRequest
--full_.wait(lock, [this] { return (queue_.size() < capacity_); });
--auto status = ScheduleRequest(request_ptr, queue_);
--empty_.notify_all();
```

#2.ScheduleRequest

```
ScheduleRequest
--if (queue.empty()) {
        queue.push(request);
        return Status::OK();
    }
--static std::map<BaseRequest::RequestType, RequestStrategyPtr> s_schedulers = {
        {BaseRequest::kSearch, std::make_shared<SearchReqStrategy>()}};
--auto iter = s_schedulers.find(request->GetRequestType());
--if (iter == s_schedulers.end() || iter->second == nullptr) {
        queue.push(request);
--else {
        iter->second->ReScheduleQueue(request, queue);
    }        
```