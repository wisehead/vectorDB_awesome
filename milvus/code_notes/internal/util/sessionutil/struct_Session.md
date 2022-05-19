#1.struct Session

```go
// Session is a struct to store service's session, including ServerID, ServerName,
// Address.
// Exclusive indicates that this server can only start one.
type Session struct {
	ctx context.Context
	// When outside context done, Session cancels its goroutines first, then uses
	// keepAliveCancel to cancel the etcd KeepAlive
	keepAliveCancel context.CancelFunc

	ServerID    int64  `json:"ServerID,omitempty"`
	ServerName  string `json:"ServerName,omitempty"`
	Address     string `json:"Address,omitempty"`
	Exclusive   bool   `json:"Exclusive,omitempty"`
	TriggerKill bool

	liveCh  <-chan bool
	etcdCli *clientv3.Client
	leaseID *clientv3.LeaseID

	metaRoot string

	registered atomic.Value
}
```