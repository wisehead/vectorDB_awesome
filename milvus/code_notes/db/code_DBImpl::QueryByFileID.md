#1.DBImpl::QueryByFileID

```
DBImpl::QueryByFileID
--// get specified files
    std::vector<size_t> ids;
    for (auto& id : file_ids) {
        std::string::size_type sz;
        ids.push_back(std::stoul(id, &sz));
    }
--auto status = meta_ptr_->FilesByID(ids, files_holder);
--milvus::engine::meta::SegmentsSchema& search_files = files_holder.HoldFiles();
--status = QueryAsync(tracer.Context(), files_holder, k, extra_params, vectors, result_ids, result_distances);
```