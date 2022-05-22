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
--// Get topic from topic begin id
--topicKeys, _, err := ri.kv.LoadWithPrefix(TopicIDTitle)
--for _, key := range topicKeys {
		topic := key[len(TopicIDTitle):]
		ri.topicRetetionTime.Store(topic, time.Now().Unix())
		topicMu.Store(topic, new(sync.Mutex))
--}	
```