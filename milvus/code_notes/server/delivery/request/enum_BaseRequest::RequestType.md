#1.enum BaseRequest::RequestType

```cpp
    enum RequestType {
        // general operations
        kCmd = 100,

        // data operations
        kInsert = 200,
        kCompact,
        kFlush,
        kDeleteByID,
        kGetVectorByID,
        kGetVectorIDs,
        kInsertEntity,

        // collection operations
        kShowCollections = 300,
        kCreateCollection,
        kHasCollection,
        kDescribeCollection,
        kCountCollection,
        kShowCollectionInfo,
        kDropCollection,
        kPreloadCollection,
        kCreateHybridCollection,
        kHasHybridCollection,
        kDescribeHybridCollection,
        kReloadSegments,

        // partition operations
        kCreatePartition = 400,
        kShowPartitions,
        kDropPartition,

        // index operations
        kCreateIndex = 500,
        kDescribeIndex,
        kDropIndex,

        // search operations
        kSearchByID = 600,
        kSearch,
        kSearchCombine,
        kHybridSearch,
    };
```