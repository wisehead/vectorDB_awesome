#1.Server.setClient

```go
	s.newDataCoordClient = func(etcdMetaRoot string, etcdCli *clientv3.Client) types.DataCoord {
		dsClient, err := dcc.NewClient(s.ctx, etcdMetaRoot, etcdCli)
		if err != nil {
			panic(err)
		}
		return dsClient
	}
	s.newIndexCoordClient = func(metaRootPath string, etcdCli *clientv3.Client) types.IndexCoord {
		isClient, err := icc.NewClient(s.ctx, metaRootPath, etcdCli)
		if err != nil {
			panic(err)
		}
		return isClient
	}
	s.newQueryCoordClient = func(metaRootPath string, etcdCli *clientv3.Client) types.QueryCoord {
		qsClient, err := qcc.NewClient(s.ctx, metaRootPath, etcdCli)
		if err != nil {
			panic(err)
		}
		return qsClient
	}
```

#2.caller

```
distributed.rootcoord.NewServer
```