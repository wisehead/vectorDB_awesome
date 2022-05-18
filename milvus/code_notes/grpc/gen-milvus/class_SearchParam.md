#1.class SearchParam

```cpp
class SearchParam :
    public ::PROTOBUF_NAMESPACE_ID::Message /* @@protoc_insertion_point(class_definition:milvus.grpc.SearchParam) */ {
  // @@protoc_insertion_point(class_scope:milvus.grpc.SearchParam)
 private:
  class _Internal;

  ::PROTOBUF_NAMESPACE_ID::internal::InternalMetadataWithArena _internal_metadata_;
  ::PROTOBUF_NAMESPACE_ID::RepeatedPtrField<std::string> partition_tag_array_;
  ::PROTOBUF_NAMESPACE_ID::RepeatedPtrField< ::milvus::grpc::RowRecord > query_record_array_;
  ::PROTOBUF_NAMESPACE_ID::RepeatedPtrField< ::milvus::grpc::KeyValuePair > extra_params_;
  ::PROTOBUF_NAMESPACE_ID::internal::ArenaStringPtr collection_name_;
  ::PROTOBUF_NAMESPACE_ID::int64 topk_;
  mutable ::PROTOBUF_NAMESPACE_ID::internal::CachedSize _cached_size_;
  friend struct ::TableStruct_milvus_2eproto;
};    
```

#2.proto

```
/**
 * @brief Params for searching vector
 */
message SearchParam {
    string collection_name = 1;
    repeated string partition_tag_array = 2;
    repeated RowRecord query_record_array = 3;
    int64 topk = 4;
    repeated KeyValuePair extra_params = 5;
}
```