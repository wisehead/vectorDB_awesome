#1.class CollectionRequestDto

```cpp
class CollectionRequestDto : public oatpp::data::mapping::type::Object {
 DTO_INIT(CollectionRequestDto, Object)

    DTO_FIELD(String, collection_name, "collection_name");
    DTO_FIELD(Int64, dimension, "dimension");
    DTO_FIELD(Int64, index_file_size, "index_file_size") = VALUE_COLLECTION_INDEX_FILE_SIZE_DEFAULT;
    DTO_FIELD(String, metric_type, "metric_type") = VALUE_COLLECTION_METRIC_TYPE_DEFAULT;
};

```