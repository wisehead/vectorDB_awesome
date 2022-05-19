#1.struct ImportTaskState

```go
type ImportTaskState struct {
	StateCode            commonpb.ImportState `protobuf:"varint,1,opt,name=stateCode,proto3,enum=milvus.proto.common.ImportState" json:"stateCode,omitempty"`
	Segments             []int64              `protobuf:"varint,2,rep,packed,name=segments,proto3" json:"segments,omitempty"`
	RowIds               []int64              `protobuf:"varint,3,rep,packed,name=row_ids,json=rowIds,proto3" json:"row_ids,omitempty"`
	RowCount             int64                `protobuf:"varint,4,opt,name=row_count,json=rowCount,proto3" json:"row_count,omitempty"`
	ErrorMessage         string               `protobuf:"bytes,5,opt,name=error_message,json=errorMessage,proto3" json:"error_message,omitempty"`
	XXX_NoUnkeyedLiteral struct{}             `json:"-"`
	XXX_unrecognized     []byte               `json:"-"`
	XXX_sizecache        int32                `json:"-"`
}
```