#1.struct GlobalTSOAllocator

```go
// GlobalTSOAllocator is the global single point TSO allocator.
type GlobalTSOAllocator struct {
	tso           *timestampOracle
	LimitMaxLogic bool
}
```