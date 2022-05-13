#1.JobMgr::worker_function

```
JobMgr::worker_function
--while (running_)
----cv_.wait(lock, [this] { return !queue_.empty(); });
----auto job = queue_.front();
----queue_.pop();
----auto tasks = build_task(job);
------JobMgr::build_task
--------TaskCreator::Create
----auto search_job = std::dynamic_pointer_cast<SearchJob>(job);
----if (search_job != nullptr)
------search_job->GetResultIds().resize(search_job->nq(), -1);
------search_job->GetResultDistances().resize(search_job->nq(), std::numeric_limits<float>::max());
------if (search_job->vectors().float_data_.empty() && search_job->vectors().binary_data_.empty() &&!search_job->vectors().id_array_.empty()) 
--------for (auto task = tasks.begin(); task != tasks.end();)
----------auto search_task = std::static_pointer_cast<XSearchTask>(*task);
----------auto location = search_task->GetLocation();   
----------// Load bloom filter
          std::string segment_dir;
          engine::utils::GetParentPath(location, segment_dir);
          segment::SegmentReader segment_reader(segment_dir);
          segment::IdBloomFilterPtr id_bloom_filter_ptr;
          segment_reader.LoadBloomFilter(id_bloom_filter_ptr);      
----------// Check if the id is present.
          bool pass = true;
          for (auto& id : search_job->vectors().id_array_) {
          	if (id_bloom_filter_ptr->Check(id)) {
            		pass = false;
            		break;
          	}
          } 
----------if (pass) {
          --search_job->SearchDone(search_task->GetIndexId());
          --task = tasks.erase(task);
----------} else {
          --task++;   
----for (auto& task : tasks) {
------OptimizerInst::GetInstance()->Run(task);
--------Optimizer::Run
----for (auto& task : tasks) {
------calculate_path(res_mgr_, task);

                          
```