#1.struct PmsFactory

```go
// PmsFactory is a pulsar msgstream factory that implemented Factory interface(msgstream.go)
type PmsFactory struct {
	dispatcherFactory ProtoUDFactory
	// the following members must be public, so that mapstructure.Decode() can access them
	PulsarAddress  string
	ReceiveBufSize int64
	PulsarBufSize  int64
}

```