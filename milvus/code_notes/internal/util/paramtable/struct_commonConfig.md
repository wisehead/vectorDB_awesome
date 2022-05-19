#1.struct commonConfig

```go
// --- common ---
type commonConfig struct {
	Base *BaseTable

	ClusterPrefix string

	ProxySubName string

	RootCoordTimeTick   string
	RootCoordStatistics string
	RootCoordDml        string
	RootCoordDelta      string
	RootCoordSubName    string

	QueryCoordSearch       string
	QueryCoordSearchResult string
	QueryCoordTimeTick     string
	QueryNodeStats         string
	QueryNodeSubName       string

	DataCoordStatistic   string
	DataCoordTimeTick    string
	DataCoordSegmentInfo string
	DataCoordSubName     string
	DataNodeSubName      string

	DefaultPartitionName string
	DefaultIndexName     string
	RetentionDuration    int64
	EntityExpirationTTL  time.Duration

	SimdType       string
	IndexSliceSize int64
	StorageType    string

	AuthorizationEnabled bool
}
```