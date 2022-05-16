#1.VectorSource::AddEntities

```
VectorSource::AddEntities
--uint64_t n = vectors_.vector_count_;
--num_entities_added = current_num_attrs_added + num_entities_to_add <= n ? num_entities_to_add : n - current_num_attrs_added;
--if (vectors_.id_array_.empty())
----SafeIDGenerator& id_generator = SafeIDGenerator::GetInstance();
----Status status = id_generator.GetNextIDNumbers(num_entities_added, vector_ids_to_add);
------SafeIDGenerator::GetNextIDNumbers
--else
----vector_ids_to_add.resize(num_entities_added);
    for (size_t pos = current_num_attrs_added; pos < current_num_attrs_added + num_entities_added; pos++) {
    	vector_ids_to_add[pos - current_num_attrs_added] = vectors_.id_array_[pos];
    }
--segment_writer_ptr->AddAttrs(collection_file_schema.collection_id_, attr_size_, attr_data_, vector_ids_to_add);
--current_num_attrs_added += num_entities_added;
--std::vector<uint8_t> vectors;
--auto size = num_entities_added * collection_file_schema.dimension_ * sizeof(float);
--vectors.resize(size);
--memcpy(vectors.data(), vectors_.float_data_.data() + current_num_vectors_added * collection_file_schema.dimension_,size);
--status = segment_writer_ptr->AddVectors(collection_file_schema.file_id_, vectors, vector_ids_to_add);
```