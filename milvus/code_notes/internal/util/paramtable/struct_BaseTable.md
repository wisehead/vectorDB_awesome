#1. struct BaseTable

```go
// BaseTable the basics of paramtable
type BaseTable struct {
	once      sync.Once
	params    *memkv.MemoryKV
	configDir string

	RoleName   string
	Log        log.Config
	LogCfgFunc func(log.Config)
}
```