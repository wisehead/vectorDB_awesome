#1.struct ServiceParam

```go
// ServiceParam is used to quickly and easily access all basic service configurations.
type ServiceParam struct {
	BaseTable

	LocalStorageCfg LocalStorageConfig
	EtcdCfg         EtcdConfig
	PulsarCfg       PulsarConfig
	KafkaCfg        KafkaConfig
	RocksmqCfg      RocksmqConfig
	MinioCfg        MinioConfig
}
```

#2.struct LocalStorageConfig

```go
type LocalStorageConfig struct {
	Base *BaseTable

	Path string
}
```

#3.struct EtcdConfig

```go

// --- etcd ---
type EtcdConfig struct {
	Base *BaseTable

	// --- ETCD ---
	Endpoints    []string
	MetaRootPath string
	KvRootPath   string
	EtcdLogLevel string
	EtcdLogPath  string

	// --- Embed ETCD ---
	UseEmbedEtcd bool
	ConfigPath   string
	DataDir      string
}
```