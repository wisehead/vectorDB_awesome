#1.struct dmlChannels

```go
type dmlChannels struct {
	ctx        context.Context
	factory    msgstream.Factory
	namePrefix string
	capacity   int64
	idx        *atomic.Int64
	pool       sync.Map
}


```