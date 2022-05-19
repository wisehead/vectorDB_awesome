#1.struct proxyConfig

```go
// --- proxy ---
type proxyConfig struct {
	Base *BaseTable

	// NetworkPort & IP are not used
	NetworkPort    int
	IP             string
	NetworkAddress string

	Alias string

	NodeID                   atomic.Value
	TimeTickInterval         time.Duration
	MsgStreamTimeTickBufSize int64
	MaxNameLength            int64
	MaxUsernameLength        int64
	MinPasswordLength        int64
	MaxPasswordLength        int64
	MaxFieldNum              int64
	MaxShardNum              int32
	MaxDimension             int64
	GinLogging               bool

	// required from QueryCoord
	SearchResultChannelNames   []string
	RetrieveResultChannelNames []string

	MaxTaskNum int64

	CreatedTime time.Time
	UpdatedTime time.Time
}
```