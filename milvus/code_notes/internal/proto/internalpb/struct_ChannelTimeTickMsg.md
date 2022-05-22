#1.struct ChannelTimeTickMsg

```go
type ChannelTimeTickMsg struct {
	Base                 *commonpb.MsgBase `protobuf:"bytes,1,opt,name=base,proto3" json:"base,omitempty"`
	ChannelNames         []string          `protobuf:"bytes,2,rep,name=channelNames,proto3" json:"channelNames,omitempty"`
	Timestamps           []uint64          `protobuf:"varint,3,rep,packed,name=timestamps,proto3" json:"timestamps,omitempty"`
	DefaultTimestamp     uint64            `protobuf:"varint,4,opt,name=default_timestamp,json=defaultTimestamp,proto3" json:"default_timestamp,omitempty"`
	XXX_NoUnkeyedLiteral struct{}          `json:"-"`
	XXX_unrecognized     []byte            `json:"-"`
	XXX_sizecache        int32             `json:"-"`
}

```