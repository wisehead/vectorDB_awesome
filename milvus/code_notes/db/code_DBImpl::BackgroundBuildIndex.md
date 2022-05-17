#1.DBImpl::BackgroundBuildIndex

```
DBImpl::BackgroundBuildIndex
--meta_ptr_->FilesToIndex(files_holder);
----MySQLMetaImpl::FilesToIndex
------statement << "SELECT id, table_id, segment_id, file_id, file_type, file_size, row_count, date,"
                      << " engine_type, created_on, updated_time"
                      << " FROM " << META_TABLEFILES << " WHERE file_type = " << std::to_string(SegmentSchema::TO_INDEX)
                      << ";";
--milvus::engine::meta::SegmentsSchema to_index_files = files_holder.HoldFiles();
--Status status = index_failed_checker_.IgnoreFailedIndexFiles(to_index_files);       
--// step 2: put build index task to scheduler
----std::vector<std::pair<scheduler::BuildIndexJobPtr, scheduler::SegmentSchemaPtr>> job2file_map;          
--for (auto& file : to_index_files) {
            scheduler::BuildIndexJobPtr job = std::make_shared<scheduler::BuildIndexJob>(meta_ptr_, options_);
            scheduler::SegmentSchemaPtr file_ptr = std::make_shared<meta::SegmentSchema>(file);
            job->AddToIndexFiles(file_ptr);
            scheduler::JobMgrInst::GetInstance()->Put(job);
            job2file_map.push_back(std::make_pair(job, file_ptr));
        }     
```