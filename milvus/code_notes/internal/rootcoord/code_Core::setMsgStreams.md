#1.Core::setMsgStreams

```
setMsgStreams
--c.SendTimeTick
--c.SendDdCreateCollectionReq 
--c.SendDdDropCollectionReq
--c.SendDdCreatePartitionReq
--c.SendDdDropPartitionReq
```

#2.c.SendTimeTick

```
c.SendTimeTick
--pc := c.chanTimeTick.listDmlChannels()
--pt := make([]uint64, len(pc))
```