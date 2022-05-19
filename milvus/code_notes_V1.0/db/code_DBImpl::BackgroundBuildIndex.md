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
----scheduler::BuildIndexJobPtr job = std::make_shared<scheduler::BuildIndexJob>(meta_ptr_, options_);
----scheduler::SegmentSchemaPtr file_ptr = std::make_shared<meta::SegmentSchema>(file);               
----job->AddToIndexFiles(file_ptr);                                                                   
----scheduler::JobMgrInst::GetInstance()->Put(job);      
------JobMgr::Put                                             
----job2file_map.push_back(std::make_pair(job, file_ptr));                                            
--}     
-- // step 3: wait build index finished and mark failed files
--for (auto iter = job2file_map.begin(); iter != job2file_map.end(); ++iter) {
----scheduler::BuildIndexJobPtr job = iter->first;
----meta::SegmentSchema& file_schema = *(iter->second.get());
----job->WaitBuildIndexFinish();
------BuildIndexJob::WaitBuildIndexFinish
--------cv_.wait(lock, [this] { return to_index_files_.empty(); });
----if (!job->GetStatus().ok()) 
------index_failed_checker_.MarkFailedIndexFile(file_schema, status.message());
----else 
------index_failed_checker_.MarkSucceedIndexFile(file_schema);
------tatus = files_holder.UnmarkFile(file_schema);
--index_req_swn_.Notify();  // notify CreateIndex check circle
```