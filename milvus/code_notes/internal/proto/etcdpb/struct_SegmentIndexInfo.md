#1.struct SegmentIndexInfo

```go
type SegmentIndexInfo struct {
	CollectionID         int64    `protobuf:"varint,1,opt,name=collectionID,proto3" json:"collectionID,omitempty"`
	PartitionID          int64    `protobuf:"varint,2,opt,name=partitionID,proto3" json:"partitionID,omitempty"`
	SegmentID            int64    `protobuf:"varint,3,opt,name=segmentID,proto3" json:"segmentID,omitempty"`
	FieldID              int64    `protobuf:"varint,4,opt,name=fieldID,proto3" json:"fieldID,omitempty"`
	IndexID              int64    `protobuf:"varint,5,opt,name=indexID,proto3" json:"indexID,omitempty"`
	BuildID              int64    `protobuf:"varint,6,opt,name=buildID,proto3" json:"buildID,omitempty"`
	EnableIndex          bool     `protobuf:"varint,7,opt,name=enable_index,json=enableIndex,proto3" json:"enable_index,omitempty"`
	XXX_NoUnkeyedLiteral struct{} `json:"-"`
	XXX_unrecognized     []byte   `json:"-"`
	XXX_sizecache        int32    `json:"-"`
}
```