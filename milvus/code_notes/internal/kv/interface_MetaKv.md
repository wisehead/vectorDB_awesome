#1.interface MetaKv

```go
// MetaKv is TxnKV for metadata. It should save data with lease.
type MetaKv interface {
	TxnKV
	GetPath(key string) string
	LoadWithPrefix(key string) ([]string, []string, error)
	LoadWithPrefix2(key string) ([]string, []string, []int64, error)
	LoadWithRevision(key string) ([]string, []string, int64, error)
	Watch(key string) clientv3.WatchChan
	WatchWithPrefix(key string) clientv3.WatchChan
	WatchWithRevision(key string, revision int64) clientv3.WatchChan
	SaveWithLease(key, value string, id clientv3.LeaseID) error
	SaveWithIgnoreLease(key, value string) error
	Grant(ttl int64) (id clientv3.LeaseID, err error)
	KeepAlive(id clientv3.LeaseID) (<-chan *clientv3.LeaseKeepAliveResponse, error)
	CompareValueAndSwap(key, value, target string, opts ...clientv3.OpOption) error
	CompareVersionAndSwap(key string, version int64, target string, opts ...clientv3.OpOption) error
}

```