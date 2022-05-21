#1.struct timestampOracle

```go
// timestampOracle is used to maintain the logic of tso.
type timestampOracle struct {
	key   string
	txnKV kv.TxnKV

	// TODO: remove saveInterval
	saveInterval  time.Duration
	maxResetTSGap func() time.Duration
	// For tso, set after the PD becomes a leader.
	TSO           unsafe.Pointer
	lastSavedTime atomic.Value
}
```