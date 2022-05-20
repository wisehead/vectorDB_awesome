#1.struct Client

```go
// Client is the datacoord grpc client
type Client struct {
	grpcClient grpcclient.GrpcClient
	sess       *sessionutil.Session
}
```