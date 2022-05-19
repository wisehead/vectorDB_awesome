#1.struct DataCoord

```
// DataCoord is the interface `datacoord` package implements
type DataCoord interface {
	Component
	TimeTickProvider

	// Flush notifies DataCoord to flush all current growing segments of specified Collection
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, which are database name(not used for now) and collection id
	//
	// response struct `FlushResponse` contains related db & collection meta
	// and the affected segment ids
	// error is returned only when some communication issue occurs
	// if some error occurs in the process of `Flush`, it will be recorded and returned in `Status` field of response
	//
	// `Flush` returns when all growing segments of specified collection is "sealed"
	// the flush procedure will wait corresponding data node(s) proceeds to the safe timestamp
	// and the `Flush` operation will be truly invoked
	// If the Datacoord or Datanode crashes in the flush procedure, recovery process will replay the ts check until all requirement is met
	//
	// Flushed segments can be check via `GetFlushedSegments` API
	Flush(ctx context.Context, req *datapb.FlushRequest) (*datapb.FlushResponse, error)

	// AssignSegmentID applies allocations for specified Coolection/Partition and related Channel Name(Virtial Channel)
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the requester's info(id and role) and the list of Assignment Request,
	// which contains the specified collection, partition id, the related VChannel Name and row count it needs
	//
	// response struct `AssignSegmentIDResponse` contains the assignment result for each request
	// error is returned only when some communication issue occurs
	// if some error occurs in the process of `AssignSegmentID`, it will be recorded and returned in `Status` field of response
	//
	// `AssignSegmentID` will applies current configured allocation policies for each request
	// if the VChannel is newly used, `WatchDmlChannels` will be invoked to notify a `DataNode`(selected by policy) to watch it
	// if there is anything make the allocation impossible, the response will not contain the corresponding result
	AssignSegmentID(ctx context.Context, req *datapb.AssignSegmentIDRequest) (*datapb.AssignSegmentIDResponse, error)

	// GetSegmentStates requests segment state information
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the list of segment id to query
	//
	// response struct `GetSegmentStatesResponse` contains the list of each state query result
	// 	when the segment is not found, the state entry will has the field `Status`  to identify failure
	// 	otherwise the Segment State and Start position information will be returned
	// error is returned only when some communication issue occurs
	GetSegmentStates(ctx context.Context, req *datapb.GetSegmentStatesRequest) (*datapb.GetSegmentStatesResponse, error)

	// GetInsertBinlogPaths requests binlog paths for specified segment
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the segment id to query
	//
	// response struct `GetInsertBinlogPathsResponse` contains the fields list
	// 	and corresponding binlog path list
	// error is returned only when some communication issue occurs
	GetInsertBinlogPaths(ctx context.Context, req *datapb.GetInsertBinlogPathsRequest) (*datapb.GetInsertBinlogPathsResponse, error)

	// GetSegmentInfoChannel DEPRECATED
	// legacy api to get SegmentInfo Channel name
	GetSegmentInfoChannel(ctx context.Context) (*milvuspb.StringResponse, error)

	// GetCollectionStatistics requests collection statistics
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the collection id to query
	//
	// response struct `GetCollectionStatisticsResponse` contains the key-value list fields returning related data
	// 	only row count for now
	// error is returned only when some communication issue occurs
	GetCollectionStatistics(ctx context.Context, req *datapb.GetCollectionStatisticsRequest) (*datapb.GetCollectionStatisticsResponse, error)

	// GetPartitionStatistics requests partition statistics
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the collection and partition id to query
	//
	// response struct `GetPartitionStatisticsResponse` contains the key-value list fields returning related data
	// 	only row count for now
	// error is returned only when some communication issue occurs
	GetPartitionStatistics(ctx context.Context, req *datapb.GetPartitionStatisticsRequest) (*datapb.GetPartitionStatisticsResponse, error)

	// GetSegmentInfo requests segment info
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the list of segment ids to query
	//
	// response struct `GetSegmentInfoResponse` contains the list of segment info
	// error is returned only when some communication issue occurs
	GetSegmentInfo(ctx context.Context, req *datapb.GetSegmentInfoRequest) (*datapb.GetSegmentInfoResponse, error)

	// GetRecoveryInfo request segment recovery info of collection/partition
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the collection/partition id to query
	//
	// response struct `GetRecoveryInfoResponse` contains the list of segments info and corresponding vchannel info
	// error is returned only when some communication issue occurs
	GetRecoveryInfo(ctx context.Context, req *datapb.GetRecoveryInfoRequest) (*datapb.GetRecoveryInfoResponse, error)

	// SaveBinlogPaths updates segments binlogs(including insert binlogs, stats logs and delta logs)
	//  and related message stream positions
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the segment binlogs and checkpoint informations.
	//
	// response status contains the status/error code and failing reason if any
	// error is returned only when some communication issue occurs
	//
	// there is a constraint that the `SaveBinlogPaths` requests of same segment shall be passed in sequence
	// 	the root reason is each `SaveBinlogPaths` will overwrite the checkpoint position
	//  if the constraint is broken, the checkpoint position will not be monotonically increasing and the integrity will be compromised
	SaveBinlogPaths(ctx context.Context, req *datapb.SaveBinlogPathsRequest) (*commonpb.Status, error)

	// GetFlushedSegments returns flushed segment list of requested collection/parition
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the collection/partition id to query
	//  when partition is lesser or equal to 0, all flushed segments of collection will be returned
	//
	// response struct `GetFlushedSegmentsResponse` contains flushed segment id list
	// error is returned only when some communication issue occurs
	GetFlushedSegments(ctx context.Context, req *datapb.GetFlushedSegmentsRequest) (*datapb.GetFlushedSegmentsResponse, error)

	// GetMetrics gets the metrics about DataCoord.
	GetMetrics(ctx context.Context, req *milvuspb.GetMetricsRequest) (*milvuspb.GetMetricsResponse, error)
	// CompleteCompaction completes a compaction with the result
	CompleteCompaction(ctx context.Context, req *datapb.CompactionResult) (*commonpb.Status, error)
	// ManualCompaction triggers a compaction for a collection
	ManualCompaction(ctx context.Context, req *milvuspb.ManualCompactionRequest) (*milvuspb.ManualCompactionResponse, error)
	// GetCompactionState gets the state of a compaction
	GetCompactionState(ctx context.Context, req *milvuspb.GetCompactionStateRequest) (*milvuspb.GetCompactionStateResponse, error)
	// GetCompactionStateWithPlans get the state of requested plan id
	GetCompactionStateWithPlans(ctx context.Context, req *milvuspb.GetCompactionPlansRequest) (*milvuspb.GetCompactionPlansResponse, error)

	// WatchChannels notifies DataCoord to watch vchannels of a collection
	WatchChannels(ctx context.Context, req *datapb.WatchChannelsRequest) (*datapb.WatchChannelsResponse, error)
	// GetFlushState gets the flush state of multiple segments
	GetFlushState(ctx context.Context, req *milvuspb.GetFlushStateRequest) (*milvuspb.GetFlushStateResponse, error)
	// SetSegmentState updates a segment's state explicitly.
	SetSegmentState(ctx context.Context, req *datapb.SetSegmentStateRequest) (*datapb.SetSegmentStateResponse, error)

	// DropVirtualChannel notifies DataCoord a virtual channel is dropped and
	// updates related segments binlogs(including insert binlogs, stats logs and delta logs)
	//  and related message stream positions
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the dropped virtual channel name and related segment information
	//
	// response status contains the status/error code and failing reason if any
	// error is returned only when some communication issue occurs
	DropVirtualChannel(ctx context.Context, req *datapb.DropVirtualChannelRequest) (*datapb.DropVirtualChannelResponse, error)

	// Import data files(json, numpy, etc.) on MinIO/S3 storage, read and parse them into sealed segments
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including file path and options
	//
	// The `Status` in response struct `ImportResponse` indicates if this operation is processed successfully or fail cause;
	// the `tasks` in `ImportResponse` return an id list of tasks.
	// error is always nil
	Import(ctx context.Context, req *datapb.ImportTaskRequest) (*datapb.ImportTaskResponse, error)

	// UpdateSegmentStatistics updates a segment's stats.
	UpdateSegmentStatistics(ctx context.Context, req *datapb.UpdateSegmentStatisticsRequest) (*commonpb.Status, error)
}

```