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
```