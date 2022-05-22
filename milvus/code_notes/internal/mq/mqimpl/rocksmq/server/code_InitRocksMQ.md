#1.InitRocksMQ

```
// InitRocksMQ init global rocksmq single instance
InitRocksMQ
--params.Init()
--fi, finalErr = os.Stat(path)
----if os.IsNotExist(finalErr) 
------finalErr = os.MkdirAll(path, os.ModePerm)
--rawRmqPageSize, err := params.Load("rocksmq.rocksmqPageSize")
--rmqPageSize, err := strconv.ParseInt(rawRmqPageSize, 10, 64)
--atomic.StoreInt64(&RocksmqPageSize, rmqPageSize)
--rawRmqRetentionTimeInMinutes, err := params.Load("rocksmq.retentionTimeInMinutes")
--rawRmqRetentionSizeInMB, err := params.Load("rocksmq.retentionSizeInMB")
--Rmq, finalErr = NewRocksMQ(path, nil)
```