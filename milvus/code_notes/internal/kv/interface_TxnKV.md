#1.interface TxnKV

```go
// TxnKV contains extra txn operations of kv. The extra operations is transactional.
type TxnKV interface {
	BaseKV
	MultiSaveAndRemove(saves map[string]string, removals []string) error
	MultiRemoveWithPrefix(keys []string) error
	MultiSaveAndRemoveWithPrefix(saves map[string]string, removals []string) error
}
```