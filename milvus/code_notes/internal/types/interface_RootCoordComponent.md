#1.interface RootCoordComponent

```go
// RootCoordComponent is used by grpc server of RootCoord
type RootCoordComponent interface {
	RootCoord

	// SetEtcdClient set EtcdClient for RootCoord
	// `etcdClient` is a client of etcd
	SetEtcdClient(etcdClient *clientv3.Client)

	// UpdateStateCode updates state code for RootCoord
	// State includes: Initializing, Healthy and Abnormal
	UpdateStateCode(internalpb.StateCode)

	// SetDataCoord set DataCoord for RootCoord
	// `dataCoord` is a client of data coordinator.
	// `ctx` is the context pass to DataCoord api.
	//
	// Always return nil.
	SetDataCoord(ctx context.Context, dataCoord DataCoord) error

	// SetIndexCoord set IndexCoord for RootCoord
	//  `indexCoord` is a client of index coordinator.
	//
	// Always return nil.
	SetIndexCoord(indexCoord IndexCoord) error

	// SetQueryCoord set QueryCoord for RootCoord
	//  `queryCoord` is a client of query coordinator.
	//
	// Always return nil.
	SetQueryCoord(queryCoord QueryCoord) error

	// SetNewProxyClient set Proxy client creator func for RootCoord
	SetNewProxyClient(func(sess *sessionutil.Session) (Proxy, error))

	// GetMetrics notifies RootCoordComponent to collect metrics for specified component
	GetMetrics(ctx context.Context, req *milvuspb.GetMetricsRequest) (*milvuspb.GetMetricsResponse, error)
}
```