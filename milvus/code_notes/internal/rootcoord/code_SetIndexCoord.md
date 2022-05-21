#1.internal.rootcoord.Core.SetIndexCoord

```
SetIndexCoord
--c.CallBuildIndexService
----rsp, err := s.BuildIndex(ctx, &indexpb.BuildIndexRequest{
			DataPaths:   binlog,
			TypeParams:  field.TypeParams,
			IndexParams: idxInfo.IndexParams,
			IndexID:     idxInfo.IndexID,
			IndexName:   idxInfo.IndexName,
			NumRows:     numRows,
			FieldSchema: field,
		})
------internal.distributed.indexcoord.client.Client::BuildIndex
--------ret, err := c.grpcClient.ReCall(ctx, func(client interface{}) (interface{}, error) {
		if !funcutil.CheckCtxValid(ctx) {
			return nil, ctx.Err()
		}
		return client.(indexpb.IndexCoordClient).BuildIndex(ctx, req)
	})
----------internal.proto.indexpb.indexCoordClient::BuildIndex
------------err := c.cc.Invoke(ctx, "/milvus.proto.index.IndexCoord/BuildIndex", in, out, opts...)		
```