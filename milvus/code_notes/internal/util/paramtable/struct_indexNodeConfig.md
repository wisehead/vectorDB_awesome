#1.struct indexNodeConfig

```go
// --- indexnode ---
type indexNodeConfig struct {
	Base *BaseTable

	IP      string
	Address string
	Port    int

	NodeID atomic.Value

	Alias string

	IndexStorageRootPath string

	CreatedTime time.Time
	UpdatedTime time.Time
}
```