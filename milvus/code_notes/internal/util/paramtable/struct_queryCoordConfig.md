#1.struct queryCoordConfig

```go
// --- querycoord ---
type queryCoordConfig struct {
	Base *BaseTable

	Address string
	Port    int
	NodeID  atomic.Value

	CreatedTime time.Time
	UpdatedTime time.Time

	//---- Handoff ---
	AutoHandoff bool

	//---- Balance ---
	AutoBalance                         bool
	OverloadedMemoryThresholdPercentage float64
	BalanceIntervalSeconds              int64
	MemoryUsageMaxDifferencePercentage  float64
}

```