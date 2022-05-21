#1.interface Allocator

```go
// Allocator is a Timestamp Oracle allocator.
type Allocator interface {
	// Initialize is used to initialize a TSO allocator.
	// It will synchronize TSO with etcd and initialize the
	// memory for later allocation work.
	Initialize() error
	// UpdateTSO is used to update the TSO in memory and the time window in etcd.
	UpdateTSO() error
	// SetTSO sets the physical part with given tso. It's mainly used for BR restore
	// and can not forcibly set the TSO smaller than now.
	SetTSO(tso uint64) error
	// GenerateTSO is used to generate a given number of TSOs.
	// Make sure you have initialized the TSO allocator before calling.
	GenerateTSO(count uint32) (uint64, error)
	// Reset is used to reset the TSO allocator.
	Reset()

	GetLastSavedTime() time.Time
}

```