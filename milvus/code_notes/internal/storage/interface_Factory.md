#1.interface Factory

```go
type Factory interface {
	NewCacheStorageChunkManager(ctx context.Context) (ChunkManager, error)
	NewVectorStorageChunkManager(ctx context.Context) (ChunkManager, error)
}
```