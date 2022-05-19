#1.interface SnapShotKV

```go
// SnapShotKV is TxnKV for snapshot data. It must save timestamp.
type SnapShotKV interface {
	Save(key string, value string, ts typeutil.Timestamp) error
	Load(key string, ts typeutil.Timestamp) (string, error)
	MultiSave(kvs map[string]string, ts typeutil.Timestamp) error
	LoadWithPrefix(key string, ts typeutil.Timestamp) ([]string, []string, error)
	MultiSaveAndRemoveWithPrefix(saves map[string]string, removals []string, ts typeutil.Timestamp) error
}

```