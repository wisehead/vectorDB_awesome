#1.struct Core

```go
// Core root coordinator core
type Core struct {
	MetaTable *MetaTable
	//id allocator
	IDAllocator       func(count uint32) (typeutil.UniqueID, typeutil.UniqueID, error)
	IDAllocatorUpdate func() error

	//tso allocator
	TSOAllocator        func(count uint32) (typeutil.Timestamp, error)
	TSOAllocatorUpdate  func() error
	TSOGetLastSavedTime func() time.Time

	//inner members
	ctx       context.Context
	cancel    context.CancelFunc
	wg        sync.WaitGroup
	etcdCli   *clientv3.Client
	kvBase    kv.TxnKV //*etcdkv.EtcdKV
	impTaskKv kv.MetaKv

	//DDL lock
	ddlLock sync.Mutex

	kvBaseCreate func(root string) (kv.TxnKV, error)

	metaKVCreate func(root string) (kv.MetaKv, error)

	//setMsgStreams, send time tick into dd channel and time tick channel
	SendTimeTick func(t typeutil.Timestamp, reason string) error

	//setMsgStreams, send create collection into dd channel
	//returns corresponding message id for each channel
	SendDdCreateCollectionReq func(ctx context.Context, req *internalpb.CreateCollectionRequest, channelNames []string) (map[string][]byte, error)

	//setMsgStreams, send drop collection into dd channel, and notify the proxy to delete this collection
	SendDdDropCollectionReq func(ctx context.Context, req *internalpb.DropCollectionRequest, channelNames []string) error

	//setMsgStreams, send create partition into dd channel
	SendDdCreatePartitionReq func(ctx context.Context, req *internalpb.CreatePartitionRequest, channelNames []string) error

	//setMsgStreams, send drop partition into dd channel
	SendDdDropPartitionReq func(ctx context.Context, req *internalpb.DropPartitionRequest, channelNames []string) error

	//get binlog file path from data service,
	CallGetBinlogFilePathsService func(ctx context.Context, segID typeutil.UniqueID, fieldID typeutil.UniqueID) ([]string, error)
	CallGetNumRowsService         func(ctx context.Context, segID typeutil.UniqueID, isFromFlushedChan bool) (int64, error)
	CallGetFlushedSegmentsService func(ctx context.Context, collID, partID typeutil.UniqueID) ([]typeutil.UniqueID, error)

	//call index builder's client to build index, return build id or get index state.
	CallBuildIndexService     func(ctx context.Context, binlog []string, field *schemapb.FieldSchema, idxInfo *etcdpb.IndexInfo, numRows int64) (typeutil.UniqueID, error)
	CallDropIndexService      func(ctx context.Context, indexID typeutil.UniqueID) error
	CallGetIndexStatesService func(ctx context.Context, IndexBuildIDs []int64) ([]*indexpb.IndexInfo, error)

	NewProxyClient func(sess *sessionutil.Session) (types.Proxy, error)

	//query service interface, notify query service to release collection
	CallReleaseCollectionService func(ctx context.Context, ts typeutil.Timestamp, dbID, collectionID typeutil.UniqueID) error
	CallReleasePartitionService  func(ctx context.Context, ts typeutil.Timestamp, dbID, collectionID typeutil.UniqueID, partitionIDs []typeutil.UniqueID) error

	// Communicates with queryCoord service for segments info.
	CallGetSegmentInfoService func(ctx context.Context, collectionID int64, segIDs []int64) (*querypb.GetSegmentInfoResponse, error)

	CallWatchChannels func(ctx context.Context, collectionID int64, channelNames []string) error

	//assign import task to data service
	CallImportService func(ctx context.Context, req *datapb.ImportTaskRequest) *datapb.ImportTaskResponse

	// Seals segments in collection cID, so they can get flushed later.
	CallFlushOnCollection func(ctx context.Context, cID int64, segIDs []int64) error

	//Proxy manager
	proxyManager *proxyManager

	// proxy clients
	proxyClientManager *proxyClientManager

	// metrics cache manager
	metricsCacheManager *metricsinfo.MetricsCacheManager

	// channel timetick
	chanTimeTick *timetickSync

	//time tick loop
	lastTimeTick typeutil.Timestamp

	//states code
	stateCode atomic.Value

	//call once
	initOnce  sync.Once
	startOnce sync.Once
	//isInit    atomic.Value

	session *sessionutil.Session

	factory dependency.Factory

	//import manager
	importManager *importManager
}

```