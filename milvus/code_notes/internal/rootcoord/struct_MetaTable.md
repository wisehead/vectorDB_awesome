#1.struct MetaTable

```go
// MetaTable store all rootCoord meta info
type MetaTable struct {
	txn             kv.TxnKV                                                        // client of a reliable txnkv service, i.e. etcd client
	snapshot        kv.SnapShotKV                                                   // client of a reliable snapshotkv service, i.e. etcd client
	proxyID2Meta    map[typeutil.UniqueID]pb.ProxyMeta                              // proxy id to proxy meta
	collID2Meta     map[typeutil.UniqueID]pb.CollectionInfo                         // collection id -> collection meta
	collName2ID     map[string]typeutil.UniqueID                                    // collection name to collection id
	collAlias2ID    map[string]typeutil.UniqueID                                    // collection alias to collection id
	partID2SegID    map[typeutil.UniqueID]map[typeutil.UniqueID]bool                // partition id -> segment_id -> bool
	segID2IndexMeta map[typeutil.UniqueID]map[typeutil.UniqueID]pb.SegmentIndexInfo // collection id/index_id/partition_id/segment_id -> meta
	indexID2Meta    map[typeutil.UniqueID]pb.IndexInfo                              // collection id/index_id -> meta

	proxyLock sync.RWMutex
	ddLock    sync.RWMutex
	credLock  sync.RWMutex
}
```