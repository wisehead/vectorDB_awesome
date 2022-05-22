#1.struct retentionInfo

```go
type retentionInfo struct {
	// key is topic name, value is last retention time
	topicRetetionTime sync.Map
	mutex             sync.RWMutex

	kv *rocksdbkv.RocksdbKV
	db *gorocksdb.DB

	closeCh   chan struct{}
	closeWg   sync.WaitGroup
	closeOnce sync.Once
}
```