#1.initRetentionInfo

```
initRetentionInfo
--ri := &retentionInfo{
		topicRetetionTime: sync.Map{},
		mutex:             sync.RWMutex{},
		kv:                kv,
		db:                db,
		closeCh:           make(chan struct{}),
		closeWg:           sync.WaitGroup{},
	}
```