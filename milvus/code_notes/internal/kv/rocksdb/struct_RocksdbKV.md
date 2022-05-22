#1.struct RocksdbKV

```go
// RocksdbKV is KV implemented by rocksdb
type RocksdbKV struct {
	Opts         *gorocksdb.Options
	DB           *gorocksdb.DB
	WriteOptions *gorocksdb.WriteOptions
	ReadOptions  *gorocksdb.ReadOptions
	name         string
}
```