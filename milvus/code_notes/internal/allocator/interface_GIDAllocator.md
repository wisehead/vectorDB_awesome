#1.interface GIDAllocator

```go
// GIDAllocator is an interface for GlobalIDAllocator.
// Alloc allocates the id of the count number.
// AllocOne allocates one id.
// UpdateID update timestamp of allocator.
type GIDAllocator interface {
	Alloc(count uint32) (UniqueID, UniqueID, error)
	AllocOne() (UniqueID, error)
	UpdateID() error
}

```