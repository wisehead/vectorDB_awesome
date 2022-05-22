#1.retentionInfo::retention

```
retention
--// Do retention check every 6s
--ticker := time.NewTicker(time.Duration(atomic.LoadInt64(&TickerTimeInSeconds) * int64(time.Second)))
--for {
----select {
----case <-ri.closeCh:
			log.Debug("Rocksmq retention finish!")
			return nil
----case t := <-ticker.C:
------ri.topicRetetionTime.Range
------func(k, v interface{}) bool
--------topic, _ := k.(string)
--------lastRetentionTs, ok := v.(int64)
--------err := ri.expiredCleanUp(topic)
--------ri.topicRetetionTime.Store(topic, timeNow)
```