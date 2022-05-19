#1.struct MemoryKV

```go
// MemoryKV implements BaseKv interface and relies on underling btree.BTree.
// As its name implies, all data is stored in memory.
type MemoryKV struct {
	sync.RWMutex
	tree *btree.BTree
}

// NewMemoryKV returns an in-memory kvBase for testing.
func NewMemoryKV() *MemoryKV {
	return &MemoryKV{
		tree: btree.New(2),
	}
}
```