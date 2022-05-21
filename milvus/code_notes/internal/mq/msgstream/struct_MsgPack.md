#1.struct MsgPack

```go
// MsgPack represents a batch of msg in msgstream
type MsgPack struct {
	BeginTs        Timestamp
	EndTs          Timestamp
	Msgs           []TsMsg
	StartPositions []*MsgPosition
	EndPositions   []*MsgPosition
}


```