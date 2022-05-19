#1.BaseTable.tryLoadFromEnv

```
BaseTable.tryLoadFromEnv
--gp.loadEtcdConfig()
----etcdEndpoints := os.Getenv("ETCD_ENDPOINTS")
----gp.Save("_EtcdEndpoints", etcdEndpoints)
--gp.loadMinioConfig()
--gp.loadMQConfig()
--gp.loadDataNodeConfig()
--gp.loadOtherEnvs()
```