#1.ComponentParam.InitOnce


```
ComponentParam.InitOnce
--p.once.Do(func() {
		p.Init()
	})
----p.Init()
```

#2.func (p *ComponentParam) Init

```
(p *ComponentParam) Init
--p.ServiceParam.Init()                                            
--p.CommonCfg.init(&p.BaseTable)      
--p.RootCoordCfg.init(&p.BaseTable)   
--p.ProxyCfg.init(&p.BaseTable)       
--p.QueryCoordCfg.init(&p.BaseTable)  
--p.QueryNodeCfg.init(&p.BaseTable)   
--p.DataCoordCfg.init(&p.BaseTable)   
--p.DataNodeCfg.init(&p.BaseTable)    
--p.IndexCoordCfg.init(&p.BaseTable)  
--p.IndexNodeCfg.init(&p.BaseTable)   

```