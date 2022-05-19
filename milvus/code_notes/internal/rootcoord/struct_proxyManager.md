#1.struct proxyManager

```go
// proxyManager manages proxy connected to the rootcoord
type proxyManager struct {
	ctx              context.Context
	cancel           context.CancelFunc
	lock             sync.Mutex
	etcdCli          *clientv3.Client
	initSessionsFunc []func([]*sessionutil.Session)
	addSessionsFunc  []func(*sessionutil.Session)
	delSessionsFunc  []func(*sessionutil.Session)
}
```