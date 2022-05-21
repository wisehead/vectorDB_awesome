#1.interface Factory

```go
type Factory interface {
	NewMsgStream(ctx context.Context) (MsgStream, error)
	NewTtMsgStream(ctx context.Context) (MsgStream, error)
	NewQueryMsgStream(ctx context.Context) (MsgStream, error)
}

```