#1.service MilvusService

```proto
service MilvusService {
    /**
     * @brief This method is used to create collection
     *
     * @param CollectionSchema, use to provide collection information to be created.
     *
     * @return Status
     */
    rpc CreateCollection(CollectionSchema) returns (Status){}

    /**
     * @brief This method is used to test collection existence.
     *
     * @param CollectionName, collection name is going to be tested.
     *
     * @return BoolReply
     */
    rpc HasCollection(CollectionName) returns (BoolReply) {}

    /**
     * @brief This method is used to get collection schema.
     *
     * @param CollectionName, target collection name.
     *
     * @return CollectionSchema
     */
    rpc DescribeCollection(CollectionName) returns (CollectionSchema) {}

    /**
     * @brief This method is used to get collection schema.
     *
     * @param CollectionName, target collection name.
     *
     * @return CollectionRowCount
     */
    rpc CountCollection(CollectionName) returns (CollectionRowCount) {}

    /**
     * @brief This method is used to list all collections.
     *
     * @param Command, dummy parameter.
     *
     * @return CollectionNameList
     */
    rpc ShowCollections(Command) returns (CollectionNameList) {}

    /**
     * @brief This method is used to get collection detail information.
     *
     * @param CollectionName, target collection name.
     *
     * @return CollectionInfo
     */
    rpc ShowCollectionInfo(CollectionName) returns (CollectionInfo) {}

    /**
     * @brief This method is used to delete collection.
     *
     * @param CollectionName, collection name is going to be deleted.
     *
     * @return CollectionNameList
     */
    rpc DropCollection(CollectionName) returns (Status) {}

    /**
     * @brief This method is used to build index by collection in sync mode.
     *
     * @param IndexParam, index paramters.
     *
     * @return Status
     */
    rpc CreateIndex(IndexParam) returns (Status) {}

    /**
     * @brief This method is used to describe index
     *
     * @param CollectionName, target collection name.
     *
     * @return IndexParam
     */
    rpc DescribeIndex(CollectionName) returns (IndexParam) {}

    /**
     * @brief This method is used to drop index
     *
     * @param CollectionName, target collection name.
     *
     * @return Status
     */
    rpc DropIndex(CollectionName) returns (Status) {}

    /**
     * @brief This method is used to create partition
     *
     * @param PartitionParam, partition parameters.
     *
     * @return Status
     */
    rpc CreatePartition(PartitionParam) returns (Status) {}

    /**
     * @brief This method is used to test partition existence.
     *
     * @param PartitionParam, target partition.
     *
     * @return BoolReply
     */
    rpc HasPartition(PartitionParam) returns (BoolReply) {}

    /**
     * @brief This method is used to show partition information
     *
     * @param CollectionName, target collection name.
     *
     * @return PartitionList
     */
    rpc ShowPartitions(CollectionName) returns (PartitionList) {}

    /**
     * @brief This method is used to drop partition
     *
     * @param PartitionParam, target partition.
     *
     * @return Status
     */
    rpc DropPartition(PartitionParam) returns (Status) {}

    /**
     * @brief This method is used to add vector array to collection.
     *
     * @param InsertParam, insert parameters.
     *
     * @return VectorIds
     */
    rpc Insert(InsertParam) returns (VectorIds) {}

    /**
     * @brief This method is used to get vectors data by id array.
     *
     * @param VectorsIdentity, target vector id array.
     *
     * @return VectorsData
     */
    rpc GetVectorsByID(VectorsIdentity) returns (VectorsData) {}

    /**
     * @brief This method is used to get vector ids from a segment
     *
     * @param GetVectorIDsParam, target collection and segment
     *
     * @return VectorIds
     */
    rpc GetVectorIDs(GetVectorIDsParam) returns (VectorIds) {}

    /**
     * @brief This method is used to query vector in collection.
     *
     * @param SearchParam, search parameters.
     *
     * @return TopKQueryResult
     */
    rpc Search(SearchParam) returns (TopKQueryResult) {}

    /**
     * @brief This method is used to query vector by id.
     *
     * @param SearchByIDParam, search parameters.
     *
     * @return TopKQueryResult
     */
    rpc SearchByID(SearchByIDParam) returns (TopKQueryResult) {}

    /**
     * @brief This method is used to query vector in specified files.
     *
     * @param SearchInFilesParam, search in files paremeters.
     *
     * @return TopKQueryResult
     */
    rpc SearchInFiles(SearchInFilesParam) returns (TopKQueryResult) {}

    /**
     * @brief This method is used to give the server status.
     *
     * @param Command, command string
     *
     * @return StringReply
     */
    rpc Cmd(Command) returns (StringReply) {}

    /**
     * @brief This method is used to delete vector by id
     *
     * @param DeleteByIDParam, delete parameters.
     *
     * @return status
     */
    rpc DeleteByID(DeleteByIDParam) returns (Status) {}

    /**
     * @brief This method is used to preload collection/partitions
     *
     * @param PreloadCollectionParam, target collection/partitions.
     *
     * @return Status
     */
    rpc PreloadCollection(PreloadCollectionParam) returns (Status) {}

    /**
     * @brief This method is used to reload collection segments
     *
     * @param ReLoadSegmentsParam, target segments information.
     *
     * @return Status
     */
    rpc ReloadSegments(ReLoadSegmentsParam) returns (Status) {}

    /**
     * @brief This method is used to flush buffer into storage.
     *
     * @param FlushParam, flush parameters
     *
     * @return Status
     */
    rpc Flush(FlushParam) returns (Status) {}

    /**
     * @brief This method is used to compact collection
     *
     * @param CollectionName, target collection name.
     *
     * @return Status
     */
    rpc Compact(CollectionName) returns (Status) {}

    /********************************New Interface********************************************/

    rpc CreateHybridCollection(Mapping) returns (Status) {}

    rpc HasHybridCollection(CollectionName) returns (BoolReply) {}

    rpc DropHybridCollection(CollectionName) returns (Status) {}

    rpc DescribeHybridCollection(CollectionName) returns (Mapping) {}

    rpc CountHybridCollection(CollectionName) returns (CollectionRowCount) {}

    rpc ShowHybridCollections(Command) returns (MappingList) {}

    rpc ShowHybridCollectionInfo (CollectionName) returns (CollectionInfo) {}

    rpc PreloadHybridCollection(CollectionName) returns (Status) {}

    ///////////////////////////////////////////////////////////////////

//    rpc CreateIndex(IndexParam) returns (Status) {}
//
//    rpc DescribeIndex(CollectionName) returns (IndexParam) {}
//
//    rpc DropIndex(CollectionName) returns (Status) {}

    ///////////////////////////////////////////////////////////////////

    rpc InsertEntity(HInsertParam) returns (HEntityIDs) {}

    // TODO(yukun): will change to HQueryResult
    rpc HybridSearch(HSearchParam) returns (TopKQueryResult) {}

    rpc HybridSearchInSegments(HSearchInSegmentsParam) returns (TopKQueryResult) {}

    rpc GetEntityByID(HEntityIdentity) returns (HEntity) {}

    rpc GetEntityIDs(HGetEntityIDsParam) returns (HEntityIDs) {}

    rpc DeleteEntitiesByID(HDeleteByIDParam) returns (Status) {}

    ///////////////////////////////////////////////////////////////////
}

```