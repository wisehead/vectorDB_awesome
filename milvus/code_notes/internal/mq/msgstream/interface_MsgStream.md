#1.interface MsgStream

```go
// MsgStream is an interface that can be used to produce and consume message on message queue
type MsgStream interface {
	Start()
	Close()

	AsProducer(channels []string)
	Produce(*MsgPack) error
	SetRepackFunc(repackFunc RepackFunc)
	ComputeProduceChannelIndexes(tsMsgs []TsMsg) [][]int32
	GetProduceChannels() []string
	ProduceMark(*MsgPack) (map[string][]MessageID, error)
	Broadcast(*MsgPack) error
	BroadcastMark(*MsgPack) (map[string][]MessageID, error)

	AsConsumer(channels []string, subName string)
	AsConsumerWithPosition(channels []string, subName string, position mqwrapper.SubscriptionInitialPosition)
	Chan() <-chan *MsgPack
	Seek(offset []*MsgPosition) error

	GetLatestMsgID(channel string) (MessageID, error)
}
```