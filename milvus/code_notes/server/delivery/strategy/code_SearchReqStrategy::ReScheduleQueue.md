#1.SearchReqStrategy::ReScheduleQueue

```
SearchReqStrategy::ReScheduleQueue
--// if config set to 0, never combine, directly put request to queue
    if (search_combine_nq_ <= 0) {
        queue.push(request);
        return Status::OK();
    }
--earchRequestPtr new_search_req = std::static_pointer_cast<SearchRequest>(request);
--if (last_req->GetRequestType() == BaseRequest::kSearch) 
----SearchRequestPtr last_search_req = std::static_pointer_cast<SearchRequest>(last_req);
----if (SearchCombineRequest::CanCombine(last_search_req, new_search_req, search_combine_nq_)) 
------// combine requests, create a SearchCombineRequest to hold them
------SearchCombineRequestPtr combine_request = std::make_shared<SearchCombineRequest>(search_combine_nq_);    
------combine_request->Combine(last_search_req);
--------SearchCombineRequest::Combine
------combine_request->Combine(new_search_req);
------queue.back() = combine_request;  // replace the last request to combine request
```