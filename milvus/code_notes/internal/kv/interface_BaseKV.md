#1.interface BaseKV

```go
// BaseKV contains base operations of kv. Include save, load and remove.
type BaseKV interface {
	Load(key string) (string, error)
	MultiLoad(keys []string) ([]string, error)
	LoadWithPrefix(key string) ([]string, []string, error)
	Save(key, value string) error
	MultiSave(kvs map[string]string) error
	Remove(key string) error
	MultiRemove(keys []string) error
	RemoveWithPrefix(key string) error

	Close()
}
```