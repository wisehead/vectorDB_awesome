#1.class KeyValuePair

```cpp
class KeyValuePair public ::PROTOBUF_NAMESPACE_ID::Message /* @@protoc_insertion_point(class_definition:milvus.grpc.KeyValuePair) */ {

  // @@protoc_insertion_point(class_scope:milvus.grpc.KeyValuePair)
 private:
  class _Internal;

  ::PROTOBUF_NAMESPACE_ID::internal::InternalMetadataWithArena _internal_metadata_;
  ::PROTOBUF_NAMESPACE_ID::internal::ArenaStringPtr key_;
  ::PROTOBUF_NAMESPACE_ID::internal::ArenaStringPtr value_;
  mutable ::PROTOBUF_NAMESPACE_ID::internal::CachedSize _cached_size_;
  friend struct ::TableStruct_milvus_2eproto;
};
```

#2.proto

```
/**
 * @brief general usage
 */
message KeyValuePair {
    string key = 1;
    string value = 2;
}

```