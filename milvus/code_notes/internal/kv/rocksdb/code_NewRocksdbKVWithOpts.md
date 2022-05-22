#1.NewRocksdbKVWithOpts

```
NewRocksdbKVWithOpts
--ro := gorocksdb.NewDefaultReadOptions()
--wo := gorocksdb.NewDefaultWriteOptions()
--// only has one columnn families
--db, err := gorocksdb.OpenDb(opts, name)
--return &RocksdbKV{
		Opts:         opts,
		DB:           db,
		WriteOptions: wo,
		ReadOptions:  ro,
		name:         name,
	}
```