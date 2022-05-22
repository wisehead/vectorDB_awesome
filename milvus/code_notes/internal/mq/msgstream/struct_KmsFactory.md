#1.struct KmsFactory

```go
type KmsFactory struct {
	dispatcherFactory ProtoUDFactory
	KafkaAddress      string
	ReceiveBufSize    int64
}
```