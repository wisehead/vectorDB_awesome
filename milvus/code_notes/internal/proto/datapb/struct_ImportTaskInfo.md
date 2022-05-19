#1.struct ImportTaskInfo

```go
type ImportTaskInfo struct {
	Id                     int64            `protobuf:"varint,1,opt,name=id,proto3" json:"id,omitempty"`
	RequestId              int64            `protobuf:"varint,2,opt,name=request_id,json=requestId,proto3" json:"request_id,omitempty"`
	DatanodeId             int64            `protobuf:"varint,3,opt,name=datanode_id,json=datanodeId,proto3" json:"datanode_id,omitempty"`
	CollectionId           int64            `protobuf:"varint,4,opt,name=collection_id,json=collectionId,proto3" json:"collection_id,omitempty"`
	PartitionId            int64            `protobuf:"varint,5,opt,name=partition_id,json=partitionId,proto3" json:"partition_id,omitempty"`
	ChannelNames           []string         `protobuf:"bytes,6,rep,name=channel_names,json=channelNames,proto3" json:"channel_names,omitempty"`
	Bucket                 string           `protobuf:"bytes,7,opt,name=bucket,proto3" json:"bucket,omitempty"`
	RowBased               bool             `protobuf:"varint,8,opt,name=row_based,json=rowBased,proto3" json:"row_based,omitempty"`
	Files                  []string         `protobuf:"bytes,9,rep,name=files,proto3" json:"files,omitempty"`
	CreateTs               int64            `protobuf:"varint,10,opt,name=create_ts,json=createTs,proto3" json:"create_ts,omitempty"`
	State                  *ImportTaskState `protobuf:"bytes,11,opt,name=state,proto3" json:"state,omitempty"`
	HeuristicDataQueryable bool             `protobuf:"varint,12,opt,name=heuristic_data_queryable,json=heuristicDataQueryable,proto3" json:"heuristic_data_queryable,omitempty"`
	HeuristicDataIndexed   bool             `protobuf:"varint,13,opt,name=heuristic_data_indexed,json=heuristicDataIndexed,proto3" json:"heuristic_data_indexed,omitempty"`
	XXX_NoUnkeyedLiteral   struct{}         `json:"-"`
	XXX_unrecognized       []byte           `json:"-"`
	XXX_sizecache          int32            `json:"-"`
}

```