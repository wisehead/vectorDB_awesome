#1.class MilvusService::Service

```cpp
class MilvusService final {
class Service : public ::grpc::Service {
   public:
    Service();
    virtual ~Service();
    // *
    // @brief This method is used to create collection
    //
    // @param CollectionSchema, use to provide collection information to be created.
    //
    // @return Status
    virtual ::grpc::Status CreateCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionSchema* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to test collection existence.
    //
    // @param CollectionName, collection name is going to be tested.
    //
    // @return BoolReply
    virtual ::grpc::Status HasCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::BoolReply* response);
    // *
    // @brief This method is used to get collection schema.
    //
    // @param CollectionName, target collection name.
    //
    // @return CollectionSchema
    virtual ::grpc::Status DescribeCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::CollectionSchema* response);
    // *
    // @brief This method is used to get collection schema.
    //
    // @param CollectionName, target collection name.
    //
    // @return CollectionRowCount
    virtual ::grpc::Status CountCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::CollectionRowCount* response);
    // *
    // @brief This method is used to list all collections.
    //
    // @param Command, dummy parameter.
    //
    // @return CollectionNameList
    virtual ::grpc::Status ShowCollections(::grpc::ServerContext* context, const ::milvus::grpc::Command* request, ::milvus::grpc::CollectionNameList* response);
    // *
    // @brief This method is used to get collection detail information.
    //
    // @param CollectionName, target collection name.
    //
    // @return CollectionInfo
    virtual ::grpc::Status ShowCollectionInfo(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::CollectionInfo* response);
    // *
    // @brief This method is used to delete collection.
    //
    // @param CollectionName, collection name is going to be deleted.
    //
    // @return CollectionNameList
    virtual ::grpc::Status DropCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to build index by collection in sync mode.
    //
    // @param IndexParam, index paramters.
    //
    // @return Status
    virtual ::grpc::Status CreateIndex(::grpc::ServerContext* context, const ::milvus::grpc::IndexParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to describe index
    //
    // @param CollectionName, target collection name.
    //
    // @return IndexParam
    virtual ::grpc::Status DescribeIndex(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::IndexParam* response);
    // *
    // @brief This method is used to drop index
    //
    // @param CollectionName, target collection name.
    //
    // @return Status
    virtual ::grpc::Status DropIndex(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to create partition
    //
    // @param PartitionParam, partition parameters.
    //
    // @return Status
    virtual ::grpc::Status CreatePartition(::grpc::ServerContext* context, const ::milvus::grpc::PartitionParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to test partition existence.
    //
    // @param PartitionParam, target partition.
    //
    // @return BoolReply
    virtual ::grpc::Status HasPartition(::grpc::ServerContext* context, const ::milvus::grpc::PartitionParam* request, ::milvus::grpc::BoolReply* response);
    // *
    // @brief This method is used to show partition information
    //
    // @param CollectionName, target collection name.
    //
    // @return PartitionList
    virtual ::grpc::Status ShowPartitions(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::PartitionList* response);
    // *
    // @brief This method is used to drop partition
    //
    // @param PartitionParam, target partition.
    //
    // @return Status
    virtual ::grpc::Status DropPartition(::grpc::ServerContext* context, const ::milvus::grpc::PartitionParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to add vector array to collection.
    //
    // @param InsertParam, insert parameters.
    //
    // @return VectorIds
    virtual ::grpc::Status Insert(::grpc::ServerContext* context, const ::milvus::grpc::InsertParam* request, ::milvus::grpc::VectorIds* response);
    // *
    // @brief This method is used to get vectors data by id array.
    //
    // @param VectorsIdentity, target vector id array.
    //
    // @return VectorsData
    virtual ::grpc::Status GetVectorsByID(::grpc::ServerContext* context, const ::milvus::grpc::VectorsIdentity* request, ::milvus::grpc::VectorsData* response);
    // *
    // @brief This method is used to get vector ids from a segment
    //
    // @param GetVectorIDsParam, target collection and segment
    //
    // @return VectorIds
    virtual ::grpc::Status GetVectorIDs(::grpc::ServerContext* context, const ::milvus::grpc::GetVectorIDsParam* request, ::milvus::grpc::VectorIds* response);
    // *
    // @brief This method is used to query vector in collection.
    //
    // @param SearchParam, search parameters.
    //
    // @return TopKQueryResult
    virtual ::grpc::Status Search(::grpc::ServerContext* context, const ::milvus::grpc::SearchParam* request, ::milvus::grpc::TopKQueryResult* response);
    // *
    // @brief This method is used to query vector by id.
    //
    // @param SearchByIDParam, search parameters.
    //
    // @return TopKQueryResult
    virtual ::grpc::Status SearchByID(::grpc::ServerContext* context, const ::milvus::grpc::SearchByIDParam* request, ::milvus::grpc::TopKQueryResult* response);
    // *
    // @brief This method is used to query vector in specified files.
    //
    // @param SearchInFilesParam, search in files paremeters.
    //
    // @return TopKQueryResult
    virtual ::grpc::Status SearchInFiles(::grpc::ServerContext* context, const ::milvus::grpc::SearchInFilesParam* request, ::milvus::grpc::TopKQueryResult* response);
    // *
    // @brief This method is used to give the server status.
    //
    // @param Command, command string
    //
    // @return StringReply
    virtual ::grpc::Status Cmd(::grpc::ServerContext* context, const ::milvus::grpc::Command* request, ::milvus::grpc::StringReply* response);
    // *
    // @brief This method is used to delete vector by id
    //
    // @param DeleteByIDParam, delete parameters.
    //
    // @return status
    virtual ::grpc::Status DeleteByID(::grpc::ServerContext* context, const ::milvus::grpc::DeleteByIDParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to preload collection/partitions
    //
    // @param PreloadCollectionParam, target collection/partitions.
    //
    // @return Status
    virtual ::grpc::Status PreloadCollection(::grpc::ServerContext* context, const ::milvus::grpc::PreloadCollectionParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to reload collection segments
    //
    // @param ReLoadSegmentsParam, target segments information.
    //
    // @return Status
    virtual ::grpc::Status ReloadSegments(::grpc::ServerContext* context, const ::milvus::grpc::ReLoadSegmentsParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to flush buffer into storage.
    //
    // @param FlushParam, flush parameters
    //
    // @return Status
    virtual ::grpc::Status Flush(::grpc::ServerContext* context, const ::milvus::grpc::FlushParam* request, ::milvus::grpc::Status* response);
    // *
    // @brief This method is used to compact collection
    //
    // @param CollectionName, target collection name.
    //
    // @return Status
    virtual ::grpc::Status Compact(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::Status* response);
    // *******************************New Interface*******************************************
    //
    virtual ::grpc::Status CreateHybridCollection(::grpc::ServerContext* context, const ::milvus::grpc::Mapping* request, ::milvus::grpc::Status* response);
    virtual ::grpc::Status HasHybridCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::BoolReply* response);
    virtual ::grpc::Status DropHybridCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::Status* response);
    virtual ::grpc::Status DescribeHybridCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::Mapping* response);
    virtual ::grpc::Status CountHybridCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::CollectionRowCount* response);
    virtual ::grpc::Status ShowHybridCollections(::grpc::ServerContext* context, const ::milvus::grpc::Command* request, ::milvus::grpc::MappingList* response);
    virtual ::grpc::Status ShowHybridCollectionInfo(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::CollectionInfo* response);
    virtual ::grpc::Status PreloadHybridCollection(::grpc::ServerContext* context, const ::milvus::grpc::CollectionName* request, ::milvus::grpc::Status* response);
    // /////////////////////////////////////////////////////////////////
    //
    //    rpc CreateIndex(IndexParam) returns (Status) {}
    //
    //    rpc DescribeIndex(CollectionName) returns (IndexParam) {}
    //
    //    rpc DropIndex(CollectionName) returns (Status) {}
    //
    // /////////////////////////////////////////////////////////////////
    //
    virtual ::grpc::Status InsertEntity(::grpc::ServerContext* context, const ::milvus::grpc::HInsertParam* request, ::milvus::grpc::HEntityIDs* response);
    // TODO(yukun): will change to HQueryResult
    virtual ::grpc::Status HybridSearch(::grpc::ServerContext* context, const ::milvus::grpc::HSearchParam* request, ::milvus::grpc::TopKQueryResult* response);
    virtual ::grpc::Status HybridSearchInSegments(::grpc::ServerContext* context, const ::milvus::grpc::HSearchInSegmentsParam* request, ::milvus::grpc::TopKQueryResult* response);
    virtual ::grpc::Status GetEntityByID(::grpc::ServerContext* context, const ::milvus::grpc::HEntityIdentity* request, ::milvus::grpc::HEntity* response);
    virtual ::grpc::Status GetEntityIDs(::grpc::ServerContext* context, const ::milvus::grpc::HGetEntityIDsParam* request, ::milvus::grpc::HEntityIDs* response);
    virtual ::grpc::Status DeleteEntitiesByID(::grpc::ServerContext* context, const ::milvus::grpc::HDeleteByIDParam* request, ::milvus::grpc::Status* response);
  };
};
```