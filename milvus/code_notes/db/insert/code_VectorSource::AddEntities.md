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
----
```