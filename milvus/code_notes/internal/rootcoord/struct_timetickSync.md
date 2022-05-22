#1.struct timetickSync

```go
type timetickSync struct {
	ctx      context.Context
	sourceID typeutil.UniqueID

	dmlChannels   *dmlChannels // used for insert
	deltaChannels *dmlChannels // used for delete

	lock           sync.Mutex
	sess2ChanTsMap map[typeutil.UniqueID]*chanTsMsg
	sendChan       chan map[typeutil.UniqueID]*chanTsMsg

	// record ddl timetick info
	ddlLock  sync.RWMutex
	ddlMinTs typeutil.Timestamp
	ddlTsSet map[typeutil.Timestamp]struct{}
}

```