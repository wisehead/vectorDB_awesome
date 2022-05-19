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

#4.struct PulsarConfig

```
// --- pulsar ---
type PulsarConfig struct {
	Base *BaseTable

	Address        string
	MaxMessageSize int
}
```

#5. struct KafkaConfig

```go
// --- kafka ---
type KafkaConfig struct {
	Base    *BaseTable
	Address string
}

```

#6. struct RocksmqConfig

```go
// --- rocksmq ---
type RocksmqConfig struct {
	Base *BaseTable

	Path string
}
```

#7. struct MinioConfig

```go
// --- minio ---
type MinioConfig struct {
	Base *BaseTable

	Address         string
	AccessKeyID     string
	SecretAccessKey string
	UseSSL          bool
	BucketName      string
	RootPath        string
}
```