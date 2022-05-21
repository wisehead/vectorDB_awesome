#1.struct GlobalIDAllocator

```go
// GlobalIDAllocator is the global single point TSO allocator.
type GlobalIDAllocator struct {
	allocator tso.Allocator
}

```