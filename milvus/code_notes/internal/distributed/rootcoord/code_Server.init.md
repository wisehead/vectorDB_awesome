#1.Server.init

```
Server.init
--Params.InitOnce(typeutil.RootCoordRole)
----GrpcServerConfig.InitOnce
------p.once.Do
--------p.init(domain)
----------GrpcServerConfig.init
------------p.grpcConfig.init(domain)
------------p.initServerMaxSendSize()
------------p.initServerMaxRecvSize()
--rootcoord.Params.InitOnce()
--rootcoord.Params.RootCoordCfg.Address = Params.GetAddress()
--rootcoord.Params.RootCoordCfg.Port = Params.Port
--etcdCli, err := etcd.GetEtcdClient(&Params.EtcdCfg)
--s.etcdCli = etcdCli
--s.rootCoord.SetEtcdClient(s.etcdCli)
--err = s.startGrpc(Params.Port)
--s.rootCoord.UpdateStateCode(internalpb.StateCode_Initializing)
--s.rootCoord.SetNewProxyClient(
		func(se *sessionutil.Session) (types.Proxy, error) {
			cli, err := pnc.NewClient(s.ctx, se.Address)
			if err != nil {
				return nil, err
			}
			if err := cli.Init(); err != nil {
				return nil, err
			}
			if err := cli.Start(); err != nil {
				return nil, err
			}
			return cli, nil
		},
	)
--dataCoord := s.newDataCoordClient(rootcoord.Params.EtcdCfg.MetaRootPath, s.etcdCli)
--err := s.rootCoord.SetDataCoord(s.ctx, dataCoord)
----Core.SetDataCoord
--s.dataCoord = dataCoord
--indexCoord := s.newIndexCoordClient(rootcoord.Params.EtcdCfg.MetaRootPath, s.etcdCli)
--err := s.rootCoord.SetIndexCoord(indexCoord);
----Core.SetIndexCoord
--s.indexCoord = indexCoord
--queryCoord := s.newQueryCoordClient(rootcoord.Params.EtcdCfg.MetaRootPath, s.etcdCli)
--err := s.rootCoord.SetQueryCoord(queryCoord);
--s.queryCoord = queryCoord
--s.rootCoord.Init()
```

#2. setClient

```go
func (s *Server) setClient() {
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
}
```