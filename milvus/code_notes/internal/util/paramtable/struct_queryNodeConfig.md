#1.struct queryNodeConfig

```go
// --- querynode ---
type queryNodeConfig struct {
	Base *BaseTable

	Alias         string
	QueryNodeIP   string
	QueryNodePort int64
	NodeID        atomic.Value
	// TODO: remove cacheSize
	CacheSize int64 // deprecated

	FlowGraphMaxQueueLength int32
	FlowGraphMaxParallelism int32

	// search
	SearchChannelNames         []string
	SearchResultChannelNames   []string
	SearchReceiveBufSize       int64
	SearchPulsarBufSize        int64
	SearchResultReceiveBufSize int64

	// Retrieve
	RetrieveChannelNames         []string
	RetrieveResultChannelNames   []string
	RetrieveReceiveBufSize       int64
	RetrievePulsarBufSize        int64
	RetrieveResultReceiveBufSize int64

	// stats
	StatsPublishInterval int

	GracefulTime int64
	SliceIndex   int

	// segcore
	ChunkRows        int64
	SmallIndexNlist  int64
	SmallIndexNProbe int64

	CreatedTime time.Time
	UpdatedTime time.Time

	// memory limit
	OverloadedMemoryThresholdPercentage float64

	// cache limit
	CacheEnabled     bool
	CacheMemoryLimit int64
}

```