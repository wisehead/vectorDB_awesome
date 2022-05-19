#1.struct Server

```go
// Server grpc wrapper
type Server struct {
	rootCoord   types.RootCoordComponent
	grpcServer  *grpc.Server
	grpcErrChan chan error

	wg sync.WaitGroup

	ctx    context.Context
	cancel context.CancelFunc

	etcdCli    *clientv3.Client
	dataCoord  types.DataCoord
	indexCoord types.IndexCoord
	queryCoord types.QueryCoord

	newIndexCoordClient func(string, *clientv3.Client) types.IndexCoord
	newDataCoordClient  func(string, *clientv3.Client) types.DataCoord
	newQueryCoordClient func(string, *clientv3.Client) types.QueryCoord

	closer io.Closer
}
```