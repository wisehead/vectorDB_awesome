#1.DBImpl::QueryAsync

```
DBImpl::QueryAsync
--milvus::engine::meta::SegmentsSchema& files = files_holder.HoldFiles();
--scheduler::SearchJobPtr job = std::make_shared<scheduler::SearchJob>(tracer.Context(), k, extra_params, vectors);
--for (auto& file : files) {
----scheduler::SegmentSchemaPtr file_ptr = std::make_shared<meta::SegmentSchema>(file);
----job->AddIndexFile(file_ptr);
--// Suspend builder
--SuspendIfFirst();
----DBImpl::SuspendIfFirst
----if (++live_search_num_ == 1)
------knowhere::BuilderSuspend();
--------faiss::BuilderSuspend::suspend();
----------BuilderSuspend::suspend
------------suspend_flag_ = true;
--// step 2: put search job to scheduler and wait result
--scheduler::JobMgrInst::GetInstance()->Put(job);
--job->WaitResult();
----SearchJob::WaitResult
------cv_.wait(lock, [this] { return index_files_.empty(); });
--// Resume builder
--ResumeIfLast();
----DBImpl::ResumeIfLast
------if (--live_search_num_ == 0) {
--------knowhere::BuildResume();
----------faiss::BuilderSuspend::resume();
------------suspend_flag_ = false;
--files_holder.ReleaseFiles();
----OngoingFileChecker::GetInstance().UnmarkOngoingFiles(hold_files_);
--// step 3: construct results
--result_ids = job->GetResultIds();
--result_distances = job->GetResultDistances();
```