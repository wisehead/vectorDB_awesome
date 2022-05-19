#1.interface Factory

```go
type Factory interface {
	Init(p *paramtable.ComponentParam)
	NewMsgStream(ctx context.Context) (msgstream.MsgStream, error)
	NewTtMsgStream(ctx context.Context) (msgstream.MsgStream, error)
	NewQueryMsgStream(ctx context.Context) (msgstream.MsgStream, error)
	NewCacheStorageChunkManager(ctx context.Context) (storage.ChunkManager, error)
	NewVectorStorageChunkManager(ctx context.Context) (storage.ChunkManager, error)
}

```