#1.struct MsgPosition

```go
type MsgPosition struct {
	ChannelName          string   `protobuf:"bytes,1,opt,name=channel_name,json=channelName,proto3" json:"channel_name,omitempty"`
	MsgID                []byte   `protobuf:"bytes,2,opt,name=msgID,proto3" json:"msgID,omitempty"`
	MsgGroup             string   `protobuf:"bytes,3,opt,name=msgGroup,proto3" json:"msgGroup,omitempty"`
	Timestamp            uint64   `protobuf:"varint,4,opt,name=timestamp,proto3" json:"timestamp,omitempty"`
	XXX_NoUnkeyedLiteral struct{} `json:"-"`
	XXX_unrecognized     []byte   `json:"-"`
	XXX_sizecache        int32    `json:"-"`
}

```