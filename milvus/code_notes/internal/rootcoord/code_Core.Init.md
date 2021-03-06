#1.internal.rootcoord.Core.Init

```
Init
--c.initOnce.Do
----c.initSession()
------c.session = sessionutil.NewSession(c.ctx, Params.EtcdCfg.MetaRootPath, c.etcdCli)
------c.session.Init(typeutil.RootCoordRole, Params.RootCoordCfg.Address, true, true)
----connectEtcdFn
------c.kvBaseCreate(Params.EtcdCfg.KvRootPath)
--------Core.kvBaseCreate
----------etcdkv.NewEtcdKV(c.etcdCli, root),
------c.metaKVCreate(Params.EtcdCfg.KvRootPath)
--------etcdkv.NewEtcdKV(c.etcdCli, root)
------c.kvBaseCreate(Params.EtcdCfg.MetaRootPath)
------newSuffixSnapshot(metaKV, "_ts", Params.EtcdCfg.MetaRootPath, "snapshots");
------NewMetaTable(metaKV, ss); 
--------mt := &MetaTable{
		txn:       txn,
		snapshot:  snap,
		proxyLock: sync.RWMutex{},
		ddLock:    sync.RWMutex{},
		credLock:  sync.RWMutex{},
	}
------err := mt.reloadFromKV()
----kv := tsoutil.NewTSOKVBase(c.etcdCli, Params.EtcdCfg.KvRootPath, "gid")
------internal.util.tsoutil.NewTSOKVBase
--------etcdkv.NewEtcdKV
----idAllocator := allocator.NewGlobalIDAllocator("idTimestamp", kv)
------allocator := tso.NewGlobalTSOAllocator(key, base)
--------return &GlobalTSOAllocator{
		tso: &timestampOracle{
			txnKV:         txnKV,
			saveInterval:  3 * time.Second,
			maxResetTSGap: func() time.Duration { return 3 * time.Second },
			key:           key,
		},
		LimitMaxLogic: true,
	}
----c.factory.Init(&Params)
------internal.util.dependency.DefaultFactory::Init
----chanMap := c.MetaTable.ListCollectionPhysicalChannels()
----c.chanTimeTick = newTimeTickSync(c.ctx, c.session.ServerID, c.factory, chanMap)
----c.chanTimeTick.addSession(c.session)
----c.proxyClientManager = newProxyClientManager(c)
----c.proxyManager = newProxyManager(
			c.ctx,
			c.etcdCli,
			c.chanTimeTick.initSessions,
			c.proxyClientManager.GetProxyClients,
		)
----c.proxyManager.AddSessionFunc(c.chanTimeTick.addSession, c.proxyClientManager.AddProxyClient)
----c.proxyManager.DelSessionFunc(c.chanTimeTick.delSession, c.proxyClientManager.DelProxyClient)

----initError = c.setMsgStreams()

----c.importManager = newImportManager(
			c.ctx,
			c.impTaskKv,
			c.IDAllocator,
			c.CallImportService,
		)
----c.importManager.init(c.ctx)

----// init data
----initError = c.initData()
```