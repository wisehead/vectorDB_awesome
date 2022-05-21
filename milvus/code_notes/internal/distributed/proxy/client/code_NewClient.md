#1.proxy.client.NewClient

```
NewClient
--ClientParams.InitOnce(typeutil.ProxyRole)
--client := &Client{
		addr: addr,
		grpcClient: &grpcclient.ClientBase{
			ClientMaxRecvSize: ClientParams.ClientMaxRecvSize,
			ClientMaxSendSize: ClientParams.ClientMaxSendSize,
			DialTimeout:       ClientParams.DialTimeout,
			KeepAliveTime:     ClientParams.KeepAliveTime,
			KeepAliveTimeout:  ClientParams.KeepAliveTimeout,
		},
	}
--client.grpcClient.SetRole(typeutil.ProxyRole)
--client.grpcClient.SetGetAddrFunc(client.getAddr)
--client.grpcClient.SetNewGrpcClientFunc(client.newGrpcClient)
```