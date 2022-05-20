#1.GetEtcdClient

```
GetEtcdClient
--GetRemoteEtcdClient
----return clientv3.New(clientv3.Config{
		Endpoints:   endpoints,
		DialTimeout: 5 * time.Second,
	})
```