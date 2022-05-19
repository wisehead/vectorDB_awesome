#1.class RowRecord

```cpp
class RowRecord :
    public ::PROTOBUF_NAMESPACE_ID::Message /* @@protoc_insertion_point(class_definition:milvus.grpc.RowRecord) */ {
 private:
  class _Internal;

  ::PROTOBUF_NAMESPACE_ID::internal::InternalMetadataWithArena _internal_metadata_;
  ::PROTOBUF_NAMESPACE_ID::RepeatedField< float > float_data_;
  mutable std::atomic<int> _float_data_cached_byte_size_;
  ::PROTOBUF_NAMESPACE_ID::internal::ArenaStringPtr binary_data_;
  mutable ::PROTOBUF_NAMESPACE_ID::internal::CachedSize _cached_size_;
  friend struct ::TableStruct_milvus_2eproto;
};    
```

#2.proto RowRecord

```
/**
 * @brief Record inserted
 */
message RowRecord {
    repeated float float_data = 1;             //float vector data
    bytes binary_data = 2;                      //binary vector data
}
```