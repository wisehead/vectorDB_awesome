#1.struct dataNodeConfig

```go
// --- datanode ---
type dataNodeConfig struct {
	Base *BaseTable

	// ID of the current node
	//NodeID atomic.Value
	NodeID atomic.Value
	// IP of the current DataNode
	IP string

	// Port of the current DataNode
	Port                    int
	FlowGraphMaxQueueLength int32
	FlowGraphMaxParallelism int32
	FlushInsertBufferSize   int64
	InsertBinlogRootPath    string
	StatsBinlogRootPath     string
	DeleteBinlogRootPath    string
	Alias                   string // Different datanode in one machine

	// etcd
	ChannelWatchSubPath string

	CreatedTime time.Time
	UpdatedTime time.Time
}

```