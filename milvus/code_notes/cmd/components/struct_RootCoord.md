#1.struct RootCoord

```go
// RootCoord implements RoodCoord grpc server
type RootCoord struct {
	ctx context.Context
	svr *rc.Server

	tracer opentracing.Tracer
	closer io.Closer
}

```