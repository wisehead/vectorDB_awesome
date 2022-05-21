#1.internal.rootcoord.Core.SetQueryCoord

```
SetQueryCoord
--c.CallReleaseCollectionService
----rsp, err := s.ReleaseCollection(ctx, req)
------internal.distributed.querycoord.client.ReleaseCollection
--------return client.(querypb.QueryCoordClient).ReleaseCollection(ctx, req)
----------internal.proto.querypb.queryCoordClient::ReleaseCollection


```