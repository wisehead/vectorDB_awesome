#1.struct chanTsMsg

```go
type chanTsMsg struct {
	chanTsMap map[string]typeutil.Timestamp
	defaultTs typeutil.Timestamp
	cnt       int64
}
```