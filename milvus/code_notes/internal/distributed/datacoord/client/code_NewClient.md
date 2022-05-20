#1.NewClient

```
NewClient
--sess := sessionutil.NewSession(ctx, metaRoot, etcdCli)
--ClientParams.InitOnce(typeutil.DataCoordRole)
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
--client.grpcClient.SetRole(typeutil.DataCoordRole)
--client.grpcClient.SetGetAddrFunc(client.getDataCoordAddr)
--client.grpcClient.SetNewGrpcClientFunc(client.newGrpcClient)
```