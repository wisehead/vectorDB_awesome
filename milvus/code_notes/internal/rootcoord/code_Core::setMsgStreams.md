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
--ttMsg := internalpb.ChannelTimeTickMsg{
			Base: &commonpb.MsgBase{
				MsgType:   commonpb.MsgType_TimeTick,
				MsgID:     0, //TODO
				Timestamp: t,
				SourceID:  c.session.ServerID,
			},
			ChannelNames:     pc,
			Timestamps:       pt,
			DefaultTimestamp: t,
		}
--c.chanTimeTick.updateTimeTick(&ttMsg, reason)
```

#2.c.SendDdCreateCollectionReq 

```
c.SendDdCreateCollectionReq 
--msgPack := ms.MsgPack{}
--baseMsg := ms.BaseMsg{
			Ctx:            ctx,
			BeginTimestamp: req.Base.Timestamp,
			EndTimestamp:   req.Base.Timestamp,
			HashValues:     []uint32{0},
		}
--msg := &ms.CreateCollectionMsg{
			BaseMsg:                 baseMsg,
			CreateCollectionRequest: *req,
		}
--msgPack.Msgs = append(msgPack.Msgs, msg)
--return c.chanTimeTick.broadcastMarkDmlChannels(channelNames, &msgPack)				
```