#1.GrpcRequestHandler::Search

```
GrpcRequestHandler::Search
--// step 1: copy vector data
--engine::VectorsData vectors;
--CopyRowRecords(request->query_record_array(), google::protobuf::RepeatedField<google::protobuf::int64>(), vectors);
----CopyRowRecords
```

#2.CopyRowRecords

```
CopyRowRecords
--
```