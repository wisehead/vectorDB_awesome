#1.internal.rootcoord.Core.SetQueryCoord

```
SetQueryCoord
--c.CallReleaseCollectionService
----rsp, err := s.ReleaseCollection(ctx, req)
------internal.distributed.querycoord.client.ReleaseCollection
--------return client.(querypb.QueryCoordClient).ReleaseCollection(ctx, req)
----------internal.proto.querypb.queryCoordClient::ReleaseCollection
------------err := c.cc.Invoke(ctx, "/milvus.proto.query.QueryCoord/ReleaseCollection", in, out, opts...)

--c.CallReleasePartitionService
----rsp, err := s.ReleasePartitions(ctx, req)
------internal.distributed.querycoord.client::ReleasePartitions
--------return client.(querypb.QueryCoordClient).ReleasePartitions(ctx, req)
----------internal.proto.querypb.queryCoordClient::ReleasePartitions
------------err := c.cc.Invoke(ctx, "/milvus.proto.query.QueryCoord/ReleasePartitions", in, out, opts...)

--c.CallGetSegmentInfoService
----resp, err := s.GetSegmentInfo(ctx, &querypb.GetSegmentInfoRequest
------internal.distributed.querycoord.client::GetSegmentInfo
--------return client.(querypb.QueryCoordClient).GetSegmentInfo(ctx, req)
	})
----------internal.proto.querypb.queryCoordClient::GetSegmentInfo
------------err := c.cc.Invoke(ctx, "/milvus.proto.query.QueryCoord/GetSegmentInfo", in, out, opts...)
```