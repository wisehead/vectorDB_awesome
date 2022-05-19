#1.struct ComponentParam

```go
// ComponentParam is used to quickly and easily access all components' configurations.
type ComponentParam struct {
	ServiceParam
	once sync.Once

	CommonCfg commonConfig

	RootCoordCfg  rootCoordConfig
	ProxyCfg      proxyConfig
	QueryCoordCfg queryCoordConfig
	QueryNodeCfg  queryNodeConfig
	DataCoordCfg  dataCoordConfig
	DataNodeCfg   dataNodeConfig
	IndexCoordCfg indexCoordConfig
	IndexNodeCfg  indexNodeConfig
}

```