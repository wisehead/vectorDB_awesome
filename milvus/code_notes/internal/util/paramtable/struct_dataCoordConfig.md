#1.struct dataCoordConfig

```go
// --- datacoord ---
type dataCoordConfig struct {
	Base *BaseTable

	NodeID atomic.Value

	IP      string
	Port    int
	Address string

	// --- ETCD ---
	ChannelWatchSubPath string

	// --- SEGMENTS ---
	SegmentMaxSize          float64
	SegmentSealProportion   float64
	SegAssignmentExpiration int64
	SegmentMaxLifetime      time.Duration

	CreatedTime time.Time
	UpdatedTime time.Time

	EnableCompaction        bool
	EnableAutoCompaction    bool
	EnableGarbageCollection bool

	// Garbage Collection
	GCInterval         time.Duration
	GCMissingTolerance time.Duration
	GCDropTolerance    time.Duration
}
```