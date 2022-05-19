#1.struct FieldSchema

```go
// @brief Field schema
type FieldSchema struct {
	FieldID              int64                    `protobuf:"varint,1,opt,name=fieldID,proto3" json:"fieldID,omitempty"`
	Name                 string                   `protobuf:"bytes,2,opt,name=name,proto3" json:"name,omitempty"`
	IsPrimaryKey         bool                     `protobuf:"varint,3,opt,name=is_primary_key,json=isPrimaryKey,proto3" json:"is_primary_key,omitempty"`
	Description          string                   `protobuf:"bytes,4,opt,name=description,proto3" json:"description,omitempty"`
	DataType             DataType                 `protobuf:"varint,5,opt,name=data_type,json=dataType,proto3,enum=milvus.proto.schema.DataType" json:"data_type,omitempty"`
	TypeParams           []*commonpb.KeyValuePair `protobuf:"bytes,6,rep,name=type_params,json=typeParams,proto3" json:"type_params,omitempty"`
	IndexParams          []*commonpb.KeyValuePair `protobuf:"bytes,7,rep,name=index_params,json=indexParams,proto3" json:"index_params,omitempty"`
	AutoID               bool                     `protobuf:"varint,8,opt,name=autoID,proto3" json:"autoID,omitempty"`
	XXX_NoUnkeyedLiteral struct{}                 `json:"-"`
	XXX_unrecognized     []byte                   `json:"-"`
	XXX_sizecache        int32                    `json:"-"`
}
```