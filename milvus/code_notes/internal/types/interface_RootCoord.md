#1.interface RootCoord

```go
// RootCoord is the interface `rootcoord` package implements
type RootCoord interface {
	Component
	TimeTickProvider

	// CreateCollection notifies RootCoord to create a collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name, collection schema and
	//     physical channel num for inserting data
	//
	// The `ErrorCode` of `Status` is `Success` if create collection successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	CreateCollection(ctx context.Context, req *milvuspb.CreateCollectionRequest) (*commonpb.Status, error)

	// DropCollection notifies RootCoord to drop a collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used) and collection name
	//
	// The `ErrorCode` of `Status` is `Success` if drop collection successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	DropCollection(ctx context.Context, req *milvuspb.DropCollectionRequest) (*commonpb.Status, error)

	// HasCollection notifies RootCoord to check a collection's existence at specified timestamp
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name and timestamp
	//
	// The `Status` in response struct `BoolResponse` indicates if this operation is processed successfully or fail cause;
	// the `Value` in `BoolResponse` is `true` if the collection exists at the specified timestamp, `false` otherwise.
	// Timestamp is ignored if set to 0.
	// error is always nil
	HasCollection(ctx context.Context, req *milvuspb.HasCollectionRequest) (*milvuspb.BoolResponse, error)

	// DescribeCollection notifies RootCoord to get all information about this collection at specified timestamp
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name or collection id, and timestamp
	//
	// The `Status` in response struct `DescribeCollectionResponse` indicates if this operation is processed successfully or fail cause;
	// other fields in `DescribeCollectionResponse` are filled with this collection's schema, collection id,
	// physical channel names, virtual channel names, created time, alias names, and so on.
	//
	// If timestamp is set a non-zero value and collection does not exist at this timestamp,
	// the `ErrorCode` of `Status` in `DescribeCollectionResponse` will be set to `Error`.
	// Timestamp is ignored if set to 0.
	// error is always nil
	DescribeCollection(ctx context.Context, req *milvuspb.DescribeCollectionRequest) (*milvuspb.DescribeCollectionResponse, error)

	// ShowCollections notifies RootCoord to list all collection names and other info in database at specified timestamp
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name and timestamp
	//
	// The `Status` in response struct `ShowCollectionsResponse` indicates if this operation is processed successfully or fail cause;
	// other fields in `ShowCollectionsResponse` are filled with all collection names, collection ids,
	// created times, created UTC times, and so on.
	// error is always nil
	ShowCollections(ctx context.Context, req *milvuspb.ShowCollectionsRequest) (*milvuspb.ShowCollectionsResponse, error)

	// CreatePartition notifies RootCoord to create a partition
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name and partition name
	//
	// The `ErrorCode` of `Status` is `Success` if create partition successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	CreatePartition(ctx context.Context, req *milvuspb.CreatePartitionRequest) (*commonpb.Status, error)

	// DropPartition notifies RootCoord to drop a partition
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name and partition name
	//
	// The `ErrorCode` of `Status` is `Success` if drop partition successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	//
	// Default partition cannot be dropped
	DropPartition(ctx context.Context, req *milvuspb.DropPartitionRequest) (*commonpb.Status, error)

	// HasPartition notifies RootCoord to check if a partition with specified name exists in the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name and partition name
	//
	// The `Status` in response struct `BoolResponse` indicates if this operation is processed successfully or fail cause;
	// the `Value` in `BoolResponse` is `true` if the partition exists in the collection, `false` otherwise.
	// error is always nil
	HasPartition(ctx context.Context, req *milvuspb.HasPartitionRequest) (*milvuspb.BoolResponse, error)

	// ShowPartitions notifies RootCoord to list all partition names and other info in the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name or collection id, and partition names
	//
	// The `Status` in response struct `ShowPartitionsResponse` indicates if this operation is processed successfully or fail cause;
	// other fields in `ShowPartitionsResponse` are filled with all partition names, partition ids,
	// created times, created UTC times, and so on.
	// error is always nil
	ShowPartitions(ctx context.Context, req *milvuspb.ShowPartitionsRequest) (*milvuspb.ShowPartitionsResponse, error)

	// CreateIndex notifies RootCoord to create an index for the specified field in the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name, field name and index parameters
	//
	// The `ErrorCode` of `Status` is `Success` if create index successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	//
	// RootCoord forwards this request to IndexCoord to create index
	CreateIndex(ctx context.Context, req *milvuspb.CreateIndexRequest) (*commonpb.Status, error)

	// DescribeIndex notifies RootCoord to get specified index information for specified field
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name, field name and index name
	//
	// The `Status` in response struct `DescribeIndexResponse` indicates if this operation is processed successfully or fail cause;
	// index information is filled in `IndexDescriptions`
	// error is always nil
	DescribeIndex(ctx context.Context, req *milvuspb.DescribeIndexRequest) (*milvuspb.DescribeIndexResponse, error)

	// DropIndex notifies RootCoord to drop the specified index for the specified field
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including database name(not used), collection name, field name and index name
	//
	// The `ErrorCode` of `Status` is `Success` if drop index successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	//
	// RootCoord forwards this request to IndexCoord to drop index
	DropIndex(ctx context.Context, req *milvuspb.DropIndexRequest) (*commonpb.Status, error)

	// CreateAlias notifies RootCoord to create an alias for the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including collection name and alias
	//
	// The `ErrorCode` of `Status` is `Success` if create alias successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	CreateAlias(ctx context.Context, req *milvuspb.CreateAliasRequest) (*commonpb.Status, error)

	// DropAlias notifies RootCoord to drop an alias for the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including alias
	//
	// The `ErrorCode` of `Status` is `Success` if drop alias successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	DropAlias(ctx context.Context, req *milvuspb.DropAliasRequest) (*commonpb.Status, error)

	// AlterAlias notifies RootCoord to alter alias for the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including collection name and new alias
	//
	// The `ErrorCode` of `Status` is `Success` if alter alias successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	AlterAlias(ctx context.Context, req *milvuspb.AlterAliasRequest) (*commonpb.Status, error)

	// AllocTimestamp notifies RootCoord to alloc timestamps
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the count of timestamps need to be allocated
	//
	// The `Status` in response struct `AllocTimestampResponse` indicates if this operation is processed successfully or fail cause;
	// `Timestamp` is the first available timestamp allocated
	// error is always nil
	AllocTimestamp(ctx context.Context, req *rootcoordpb.AllocTimestampRequest) (*rootcoordpb.AllocTimestampResponse, error)

	// AllocID notifies RootCoord to alloc IDs
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the count of IDs need to be allocated
	//
	// The `Status` in response struct `AllocTimestampResponse` indicates if this operation is processed successfully or fail cause;
	// `ID` is the first available id allocated
	// error is always nil
	AllocID(ctx context.Context, req *rootcoordpb.AllocIDRequest) (*rootcoordpb.AllocIDResponse, error)

	// UpdateChannelTimeTick notifies RootCoord to update each Proxy's safe timestamp
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including physical channel names, channels' safe timestamps and default timestamp
	//
	// The `ErrorCode` of `Status` is `Success` if update channel timetick successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	UpdateChannelTimeTick(ctx context.Context, req *internalpb.ChannelTimeTickMsg) (*commonpb.Status, error)

	// DescribeSegment notifies RootCoord to get specified segment information in the collection
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including collection id and segment id
	//
	// The `Status` in response struct `DescribeSegmentResponse` indicates if this operation is processed successfully or fail cause;
	// segment index information is filled in `IndexID`, `BuildID` and `EnableIndex`.
	// error is always nil
	DescribeSegment(ctx context.Context, req *milvuspb.DescribeSegmentRequest) (*milvuspb.DescribeSegmentResponse, error)

	// ShowSegments notifies RootCoord to list all segment ids in the collection or partition
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including collection id and partition id
	//
	// The `Status` in response struct `ShowSegmentsResponse` indicates if this operation is processed successfully or fail cause;
	// `SegmentIDs` in `ShowSegmentsResponse` records all segment ids.
	// error is always nil
	ShowSegments(ctx context.Context, req *milvuspb.ShowSegmentsRequest) (*milvuspb.ShowSegmentsResponse, error)

	DescribeSegments(ctx context.Context, in *rootcoordpb.DescribeSegmentsRequest) (*rootcoordpb.DescribeSegmentsResponse, error)

	// ReleaseDQLMessageStream notifies RootCoord to release and close the search message stream of specific collection.
	//
	// ctx is the request to control request deadline and cancellation.
	// request contains the request params, which are database id(not used) and collection id.
	//
	// The `ErrorCode` of `Status` is `Success` if drop index successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	//
	// RootCoord just forwards this request to Proxy client
	ReleaseDQLMessageStream(ctx context.Context, in *proxypb.ReleaseDQLMessageStreamRequest) (*commonpb.Status, error)

	// SegmentFlushCompleted notifies RootCoord that specified segment has been flushed
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including SegmentInfo
	//
	// The `ErrorCode` of `Status` is `Success` if process successfully;
	// otherwise, the `ErrorCode` of `Status` will be `Error`, and the `Reason` of `Status` will record the fail cause.
	// error is always nil
	//
	// This interface is only used by DataCoord, when RootCoord receives this request, RootCoord will notify IndexCoord
	// to build index for this segment.
	SegmentFlushCompleted(ctx context.Context, in *datapb.SegmentFlushCompletedMsg) (*commonpb.Status, error)

	// GetMetrics notifies RootCoord to collect metrics for specified component
	GetMetrics(ctx context.Context, req *milvuspb.GetMetricsRequest) (*milvuspb.GetMetricsResponse, error)

	// Import data files(json, numpy, etc.) on MinIO/S3 storage, read and parse them into sealed segments
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including file path and options
	//
	// Return status indicates if this operation is processed successfully or fail cause;
	// error is always nil
	Import(ctx context.Context, req *milvuspb.ImportRequest) (*milvuspb.ImportResponse, error)

	// GetImportState checks import task state from datanode
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params, including a task id
	//
	// The `Status` in response struct `GetImportStateResponse` indicates if this operation is processed successfully or fail cause;
	// the `state` in `GetImportStateResponse` return the state of the import task.
	// error is always nil
	GetImportState(ctx context.Context, req *milvuspb.GetImportStateRequest) (*milvuspb.GetImportStateResponse, error)

	// List id array of all import tasks
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the request params
	//
	// The `Status` in response struct `ListImportTasksResponse` indicates if this operation is processed successfully or fail cause;
	// the `Tasks` in `ListImportTasksResponse` return the id array of all import tasks.
	// error is always nil
	ListImportTasks(ctx context.Context, req *milvuspb.ListImportTasksRequest) (*milvuspb.ListImportTasksResponse, error)

	// ReportImport reports import task state to rootCoord
	//
	// ctx is the context to control request deadline and cancellation
	// req contains the import results, including imported row count and an id list of generated segments
	//
	// response status contains the status/error code and failing reason if any error is returned
	// error is always nil
	ReportImport(ctx context.Context, req *rootcoordpb.ImportResult) (*commonpb.Status, error)

	// CreateCredential create new user and password
	CreateCredential(ctx context.Context, req *internalpb.CredentialInfo) (*commonpb.Status, error)
	// UpdateCredential update password for a user
	UpdateCredential(ctx context.Context, req *internalpb.CredentialInfo) (*commonpb.Status, error)
	// DeleteCredential delete a user
	DeleteCredential(ctx context.Context, req *milvuspb.DeleteCredentialRequest) (*commonpb.Status, error)
	// ListCredUsers list all usernames
	ListCredUsers(ctx context.Context, req *milvuspb.ListCredUsersRequest) (*milvuspb.ListCredUsersResponse, error)
	// GetCredential get credential by username
	GetCredential(ctx context.Context, req *rootcoordpb.GetCredentialRequest) (*rootcoordpb.GetCredentialResponse, error)
}

```