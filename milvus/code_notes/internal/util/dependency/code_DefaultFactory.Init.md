#1.DefaultFactory.Init

```
// Init create a msg factory(TODO only support one mq at the same time.)
// In order to guarantee backward compatibility of config file, we still support multiple mq configs.
// 1. Rocksmq only run on local mode, and it has the highest priority
// 2. Pulsar has higher priority than Kafka within remote msg

DefaultFactory.Init
--// init storage
--if params.CommonCfg.StorageType == "local" {
----f.chunkManagerFactory = storage.NewChunkManagerFactory("local", "local",
			storage.RootPath(params.LocalStorageCfg.Path))
--} else {
----f.chunkManagerFactory = storage.NewChunkManagerFactory("local", "minio",
			storage.RootPath(params.LocalStorageCfg.Path),
			storage.Address(params.MinioCfg.Address),
			storage.AccessKeyID(params.MinioCfg.AccessKeyID),
			storage.SecretAccessKeyID(params.MinioCfg.SecretAccessKey),
			storage.UseSSL(params.MinioCfg.UseSSL),
			storage.BucketName(params.MinioCfg.BucketName),
			storage.CreateBucket(true))
	}
--// init mq storage
--if f.standAlone
----f.msgStreamFactory = f.initMQLocalService(params)
----if f.msgStreamFactory == nil {
------f.msgStreamFactory = f.initMQRemoteService(params)
--f.msgStreamFactory = f.initMQRemoteService(params)
```