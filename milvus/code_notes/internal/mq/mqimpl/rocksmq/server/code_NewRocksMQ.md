#1.NewRocksMQ

```
// NewRocksMQ step:
// 1. New rocksmq instance based on rocksdb with name and rocksdbkv with kvname
// 2. Init retention info, load retention info to memory
// 3. Start retention goroutine

NewRocksMQ
--bbto := gorocksdb.NewDefaultBlockBasedTableOptions()
--bbto.SetBlockCache(gorocksdb.NewLRUCache(RocksDBLRUCacheCapacity))
--optsKV := gorocksdb.NewDefaultOptions()
--optsKV.SetBlockBasedTableFactory(bbto)
--optsKV.SetCreateIfMissing(true)
--// by default there are only 1 thread for flush compaction, which may block each other.
--// increase to a reasonable thread numbers
--optsKV.IncreaseParallelism(parallelism)
--// enable back ground flush
--optsKV.SetMaxBackgroundFlushes(1)

// finish rocks KV
--kvName := name + kvSuffix
--kv, err := rocksdbkv.NewRocksdbKVWithOpts(kvName, optsKV)

--// finish rocks mq store initialization, rocks mq store has to set the prefix extractor
--optsStore := gorocksdb.NewDefaultOptions()
--// share block cache with kv
--optsStore.SetBlockBasedTableFactory(bbto)
--optsStore.SetCreateIfMissing(true)
	// by default there are only 1 thread for flush compaction, which may block each other.
	// increase to a reasonable thread numbers
--optsStore.IncreaseParallelism(parallelism)
	// enable back ground flush
--optsStore.SetMaxBackgroundFlushes(1)

--db, err := gorocksdb.OpenDb(optsStore, name)

--rmq := &rocksmq{
		store:       db,
		kv:          kv,
		idAllocator: mqIDAllocator,
		storeMu:     &sync.Mutex{},
		consumers:   sync.Map{},
		readers:     sync.Map{},
	}

--ri, err := initRetentionInfo(kv, db)
--if checkRetention() {
		rmq.retentionInfo.startRetentionInfo()
	}
--atomic.StoreInt64(&rmq.state, RmqStateHealthy)
```