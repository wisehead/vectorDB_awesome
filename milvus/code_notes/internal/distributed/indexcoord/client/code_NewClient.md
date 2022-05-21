#1.NewClient

```
NewClient
--sess := sessionutil.NewSession(ctx, metaRoot, etcdCli)
--ClientParams.InitOnce(typeutil.IndexCoordRole)
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
--client.grpcClient.SetRole(typeutil.IndexCoordRole)
	client.grpcClient.SetGetAddrFunc(client.getIndexCoordAddr)
	client.grpcClient.SetNewGrpcClientFunc(client.newGrpcClient)	
```