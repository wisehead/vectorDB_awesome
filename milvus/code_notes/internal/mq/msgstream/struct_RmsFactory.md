#1.struct RmsFactory

```go
// RmsFactory is a rocksmq msgstream factory that implemented Factory interface(msgstream.go)
type RmsFactory struct {
	dispatcherFactory ProtoUDFactory
	// the following members must be public, so that mapstructure.Decode() can access them
	ReceiveBufSize int64
	RmqBufSize     int64
}
```