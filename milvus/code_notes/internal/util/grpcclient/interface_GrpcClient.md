#1.interface GrpcClient

```go
// GrpcClient abstracts client of grpc
type GrpcClient interface {
	SetRole(string)
	GetRole() string
	SetGetAddrFunc(func() (string, error))
	SetNewGrpcClientFunc(func(cc *grpc.ClientConn) interface{})
	GetGrpcClient(ctx context.Context) (interface{}, error)
	ReCall(ctx context.Context, caller func(client interface{}) (interface{}, error)) (interface{}, error)
	Call(ctx context.Context, caller func(client interface{}) (interface{}, error)) (interface{}, error)
	Close() error
}
```