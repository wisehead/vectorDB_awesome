#1.interface Proxy

```go
// Proxy is the interface `proxy` package implements
type Proxy interface {
	Component

	// InvalidateCollectionMetaCache notifies Proxy to clear all the meta cache of specific collection.
	//
	// InvalidateCollectionMetaCache should be called when there are any meta changes in specific collection.
	// Such as `DropCollection`, `CreatePartition`, `DropPartition`, etc.
	//
	// ctx is the request to control request deadline and cancellation.
	// request contains the request params, which are database name(not used now) and collection name.
	//
	// InvalidateCollectionMetaCache should always succeed even though the specific collection doesn't exist in Proxy.
	// So the code of response `Status` should be always `Success`.
	//
	// error is returned only when some communication issue occurs.
	InvalidateCollectionMetaCache(ctx context.Context, request *proxypb.InvalidateCollMetaCacheRequest) (*commonpb.Status, error)

	// InvalidateCredentialCache notifies Proxy to clear all the credential cache of specified username.
	//
	// InvalidateCredentialCache should be called when there are credential changes for specified username.
	// Such as `CreateCredential`, `UpdateCredential`, `DeleteCredential`, etc.
	//
	// InvalidateCredentialCache should always succeed even though the specified username doesn't exist in Proxy.
	// So the code of response `Status` should be always `Success`.
	//
	// error is returned only when some communication issue occurs.
	InvalidateCredentialCache(ctx context.Context, request *proxypb.InvalidateCredCacheRequest) (*commonpb.Status, error)

	UpdateCredentialCache(ctx context.Context, request *proxypb.UpdateCredCacheRequest) (*commonpb.Status, error)

	ClearCredUsersCache(ctx context.Context, request *internalpb.ClearCredUsersCacheRequest) (*commonpb.Status, error)

	// ReleaseDQLMessageStream notifies Proxy to release and close the search message stream of specific collection.
	//
	// ReleaseDQLMessageStream should be called when the specific collection was released.
	//
	// ctx is the request to control request deadline and cancellation.
	// request contains the request params, which are database id(not used now) and collection id.
	//
	// ReleaseDQLMessageStream should always succeed even though the specific collection doesn't exist in Proxy.
	// So the code of response `Status` should be always `Success`.
	//
	// error is returned only when some communication issue occurs.
	ReleaseDQLMessageStream(ctx context.Context, in *proxypb.ReleaseDQLMessageStreamRequest) (*commonpb.Status, error)

	SendSearchResult(ctx context.Context, req *internalpb.SearchResults) (*commonpb.Status, error)
	SendRetrieveResult(ctx context.Context, req *internalpb.RetrieveResults) (*commonpb.Status, error)
}
```