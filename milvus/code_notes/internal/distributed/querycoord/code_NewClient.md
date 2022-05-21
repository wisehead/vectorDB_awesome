#1.querycoord.client.NewClient

```
NewClient
--sess := sessionutil.NewSession(ctx, metaRoot, etcdCli)
--ClientParams.InitOnce(typeutil.QueryCoordRole)
--client := &Client{
		grpcClient: &grpcclient.ClientBase{
			ClientMaxRecvSize: ClientParams.ClientMaxRecvSize,
			ClientMaxSendSize: ClientParams.ClientMaxSendSize,
			DialTimeout:       ClientParams.DialTimeout,
			KeepAliveTime:     ClientParams.KeepAliveTime,
			KeepAliveTimeout:  ClientParams.KeepAliveTimeout,
		},
		sess: sess,
	}
--client.grpcClient.SetRole(typeutil.QueryCoordRole)
--client.grpcClient.SetGetAddrFunc(client.getQueryCoordAddr)
--client.grpcClient.SetNewGrpcClientFunc(client.newGrpcClient)
```