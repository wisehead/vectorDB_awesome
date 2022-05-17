#1.GrpcRequestHandler::CreateCollection

```
GrpcRequestHandler::CreateCollection
--Status status = request_handler_.CreateCollection(GetContext(context), request->collection_name(), request->dimension(),
                                          request->index_file_size(), request->metric_type());
----RequestHandler::CreateCollection
------BaseRequestPtr request_ptr =CreateCollectionRequest::Create(context, collection_name, dimension, index_file_size, metric_type);
------RequestScheduler::ExecRequest(request_ptr);
--------RequestScheduler::ExecRequest
----------RequestScheduler& scheduler = RequestScheduler::GetInstance();
----------scheduler.ExecuteRequest(request_ptr);
--SET_RESPONSE(response, status, context);
```