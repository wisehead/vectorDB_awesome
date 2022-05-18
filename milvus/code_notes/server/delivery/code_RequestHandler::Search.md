#1.RequestHandler::Search

```
RequestHandler::Search
--BaseRequestPtr request_ptr = SearchRequest::Create(context, collection_name, vectors, topk, extra_params,
                                                       partition_list, file_id_list, result);
--RequestScheduler::ExecRequest(request_ptr);
----RequestScheduler::ExecRequest
------scheduler.ExecuteRequest(request_ptr);
--------RequestScheduler::ExecuteRequest
```