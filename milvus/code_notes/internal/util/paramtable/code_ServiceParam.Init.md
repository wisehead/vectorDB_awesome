#1.ServiceParam.Init

```
ServiceParam.Init
--p.BaseTable.Init()                                         
--p.LocalStorageCfg.init(&p.BaseTable)  
----LocalStorageConfig.init
------LocalStorageConfig.initPath
--------p.Path = p.Base.LoadWithDefault("localStorage.path", "/var/lib/milvus/data")
----------gp.params.LoadWithDefault(strings.ToLower(key), defaultValue)
------------MemoryKV.LoadWithDefault
--------------item := kv.tree.Get(memoryKVItem{key: key})
--p.EtcdCfg.init(&p.BaseTable) 
----EtcdConfig.init
------EtcdConfig.LoadCfgToMemory
--------initUseEmbedEtcd
--------if p.UseEmbedEtcd {   
--------	p.initConfigPath()  
--------	p.initDataDir()     
--------} else {              
--------	p.initEndpoints()   
--------}                     
--------p.initMetaRootPath()  
--------p.initKvRootPath()    
--------p.initEtcdLogLevel()  
--------p.initEtcdLogPath()   
--p.PulsarCfg.init(&p.BaseTable)        
--p.KafkaCfg.init(&p.BaseTable)         
--p.RocksmqCfg.init(&p.BaseTable)       
--p.MinioCfg.init(&p.BaseTable)         

```