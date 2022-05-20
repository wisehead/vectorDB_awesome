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
```