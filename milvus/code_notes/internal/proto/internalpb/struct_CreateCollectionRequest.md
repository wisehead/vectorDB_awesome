#1.strucrt CreateCollectionRequest

```go
type CreateCollectionRequest struct {
	Base           *commonpb.MsgBase `protobuf:"bytes,1,opt,name=base,proto3" json:"base,omitempty"`
	DbName         string            `protobuf:"bytes,2,opt,name=db_name,json=dbName,proto3" json:"db_name,omitempty"`
	CollectionName string            `protobuf:"bytes,3,opt,name=collectionName,proto3" json:"collectionName,omitempty"`
	PartitionName  string            `protobuf:"bytes,4,opt,name=partitionName,proto3" json:"partitionName,omitempty"`
	// `schema` is the serialized `schema.CollectionSchema`
	DbID                 int64    `protobuf:"varint,5,opt,name=dbID,proto3" json:"dbID,omitempty"`
	CollectionID         int64    `protobuf:"varint,6,opt,name=collectionID,proto3" json:"collectionID,omitempty"`
	PartitionID          int64    `protobuf:"varint,7,opt,name=partitionID,proto3" json:"partitionID,omitempty"`
	Schema               []byte   `protobuf:"bytes,8,opt,name=schema,proto3" json:"schema,omitempty"`
	VirtualChannelNames  []string `protobuf:"bytes,9,rep,name=virtualChannelNames,proto3" json:"virtualChannelNames,omitempty"`
	PhysicalChannelNames []string `protobuf:"bytes,10,rep,name=physicalChannelNames,proto3" json:"physicalChannelNames,omitempty"`
	XXX_NoUnkeyedLiteral struct{} `json:"-"`
	XXX_unrecognized     []byte   `json:"-"`
	XXX_sizecache        int32    `json:"-"`
}
```