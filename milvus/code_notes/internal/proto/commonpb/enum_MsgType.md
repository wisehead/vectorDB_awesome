#1.enum MsgType

```go
const (
	MsgType_Undefined MsgType = 0
	// DEFINITION REQUESTS: COLLECTION
	MsgType_CreateCollection   MsgType = 100
	MsgType_DropCollection     MsgType = 101
	MsgType_HasCollection      MsgType = 102
	MsgType_DescribeCollection MsgType = 103
	MsgType_ShowCollections    MsgType = 104
	MsgType_GetSystemConfigs   MsgType = 105
	MsgType_LoadCollection     MsgType = 106
	MsgType_ReleaseCollection  MsgType = 107
	MsgType_CreateAlias        MsgType = 108
	MsgType_DropAlias          MsgType = 109
	MsgType_AlterAlias         MsgType = 110
	// DEFINITION REQUESTS: PARTITION
	MsgType_CreatePartition   MsgType = 200
	MsgType_DropPartition     MsgType = 201
	MsgType_HasPartition      MsgType = 202
	MsgType_DescribePartition MsgType = 203
	MsgType_ShowPartitions    MsgType = 204
	MsgType_LoadPartitions    MsgType = 205
	MsgType_ReleasePartitions MsgType = 206
	// DEFINE REQUESTS: SEGMENT
	MsgType_ShowSegments        MsgType = 250
	MsgType_DescribeSegment     MsgType = 251
	MsgType_LoadSegments        MsgType = 252
	MsgType_ReleaseSegments     MsgType = 253
	MsgType_HandoffSegments     MsgType = 254
	MsgType_LoadBalanceSegments MsgType = 255
	MsgType_DescribeSegments    MsgType = 256
	// DEFINITION REQUESTS: INDEX
	MsgType_CreateIndex   MsgType = 300
	MsgType_DescribeIndex MsgType = 301
	MsgType_DropIndex     MsgType = 302
	// MANIPULATION REQUESTS
	MsgType_Insert MsgType = 400
	MsgType_Delete MsgType = 401
	MsgType_Flush  MsgType = 402
	// QUERY
	MsgType_Search                   MsgType = 500
	MsgType_SearchResult             MsgType = 501
	MsgType_GetIndexState            MsgType = 502
	MsgType_GetIndexBuildProgress    MsgType = 503
	MsgType_GetCollectionStatistics  MsgType = 504
	MsgType_GetPartitionStatistics   MsgType = 505
	MsgType_Retrieve                 MsgType = 506
	MsgType_RetrieveResult           MsgType = 507
	MsgType_WatchDmChannels          MsgType = 508
	MsgType_RemoveDmChannels         MsgType = 509
	MsgType_WatchQueryChannels       MsgType = 510
	MsgType_RemoveQueryChannels      MsgType = 511
	MsgType_SealedSegmentsChangeInfo MsgType = 512
	MsgType_WatchDeltaChannels       MsgType = 513
	MsgType_GetShardLeaders          MsgType = 514
	MsgType_GetReplicas              MsgType = 515
	// DATA SERVICE
	MsgType_SegmentInfo     MsgType = 600
	MsgType_SystemInfo      MsgType = 601
	MsgType_GetRecoveryInfo MsgType = 602
	MsgType_GetSegmentState MsgType = 603
	// SYSTEM CONTROL
	MsgType_TimeTick          MsgType = 1200
	MsgType_QueryNodeStats    MsgType = 1201
	MsgType_LoadIndex         MsgType = 1202
	MsgType_RequestID         MsgType = 1203
	MsgType_RequestTSO        MsgType = 1204
	MsgType_AllocateSegment   MsgType = 1205
	MsgType_SegmentStatistics MsgType = 1206
	MsgType_SegmentFlushDone  MsgType = 1207
	MsgType_DataNodeTt        MsgType = 1208
	// Credential
	MsgType_CreateCredential  MsgType = 1500
	MsgType_GetCredential     MsgType = 1501
	MsgType_DeleteCredential  MsgType = 1502
	MsgType_UpdateCredential  MsgType = 1503
	MsgType_ListCredUsernames MsgType = 1504
)
```