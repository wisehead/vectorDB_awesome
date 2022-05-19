#1.struct ProxyMeta

```go
type ProxyMeta struct {
	ID                   int64             `protobuf:"varint,1,opt,name=ID,proto3" json:"ID,omitempty"`
	Address              *commonpb.Address `protobuf:"bytes,2,opt,name=address,proto3" json:"address,omitempty"`
	ResultChannelIDs     []string          `protobuf:"bytes,3,rep,name=result_channelIDs,json=resultChannelIDs,proto3" json:"result_channelIDs,omitempty"`
	XXX_NoUnkeyedLiteral struct{}          `json:"-"`
	XXX_unrecognized     []byte            `json:"-"`
	XXX_sizecache        int32             `json:"-"`
}
```