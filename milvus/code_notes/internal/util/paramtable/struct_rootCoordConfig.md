#1.struct rootCoordConfig

```go
// --- rootcoord ---
type rootCoordConfig struct {
	Base *BaseTable

	Address string
	Port    int

	DmlChannelNum                   int64
	MaxPartitionNum                 int64
	MinSegmentSizeToEnableIndex     int64
	ImportTaskExpiration            float64
	ImportTaskRetention             float64
	ImportSegmentStateCheckInterval float64
	ImportSegmentStateWaitLimit     float64
	ImportIndexCheckInterval        float64
	ImportIndexWaitLimit            float64

	// --- ETCD Path ---
	ImportTaskSubPath string

	CreatedTime time.Time
	UpdatedTime time.Time
}

```