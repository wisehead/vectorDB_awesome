#1.GrpcServerConfig.init

```
GrpcServerConfig.init
--p.grpcConfig.init(domain)
----grpcConfig.init
------
--p.initServerMaxSendSize()
--p.initServerMaxRecvSize()
```

```
grpcConfig.init
--p.ServiceParam.Init()
--p.Domain = domain
--p.LoadFromEnv()
----ipv4.LocalIP()
------addrs, err := net.InterfaceAddrs()
--p.LoadFromArgs()
--p.initPort()
----p.Port = p.ParseIntWithDefault(p.Domain+".port", ProxyExternalPort)
----p.InternalPort = p.ParseIntWithDefault(p.Domain+".internalPort", ProxyInternalPort)
--p.initTLSPath()
----p.TLSEnabled = p.ParseBool("common.security.tlsEnabled", false)
	p.ServerPemPath = p.Get("tls.serverPemPath")
	p.ServerKeyPath = p.Get("tls.serverKeyPath")
	p.CaPemPath = p.Get("tls.caPemPath")
}
```