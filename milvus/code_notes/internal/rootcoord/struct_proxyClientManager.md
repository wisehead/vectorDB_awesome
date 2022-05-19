#1.struct proxyClientManager

```go
type proxyClientManager struct {
	core        *Core
	lock        sync.RWMutex
	proxyClient map[int64]types.Proxy
	helper      proxyClientManagerHelper
}
```