#1.SearchReqStrategy::ReScheduleQueue

```
SearchReqStrategy::ReScheduleQueue
--// if config set to 0, never combine, directly put request to queue
    if (search_combine_nq_ <= 0) {
        queue.push(request);
        return Status::OK();
    }
--earchRequestPtr new_search_req = std::static_pointer_cast<SearchRequest>(request);    
```