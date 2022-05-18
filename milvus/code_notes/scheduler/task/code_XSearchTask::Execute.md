#1.XSearchTask::Execute

```
XSearchTask::Execute
--auto job = job_.lock()
--auto search_job = std::static_pointer_cast<scheduler::SearchJob>(job);
--// step 1: allocate memory
--query::GeneralQueryPtr general_query = search_job->general_query();
--uint64_t nq = search_job->nq();
--uint64_t topk = search_job->topk();
--const milvus::json& extra_params = search_job->extra_params();
--const engine::VectorsData& vectors = search_job->vectors();
--auto engine_type = index_engine_->IndexEngineType();
--if (engine_type == EngineType::FAISS_IDMAP || engine_type == EngineType::FAISS_BIN_IDMAP) 
----// allow to assign a metric type in IDMAP and BIN_IDMAP
----if (extra_params.contains(knowhere::Metric::TYPE)) 
------auto metric_type = extra_params[knowhere::Metric::TYPE].get<int64_t>();
------if (engine_type == EngineType::FAISS_IDMAP) {
                    if (metric_type == static_cast<int64_t>(MetricType::IP)) {
                        ascending_reduce = false;
                    } else if (metric_type == static_cast<int64_t>(MetricType::L2)) {
                        // do nothing
                    } else {
                        Illegal_Metric_Type();
                        return;
                    }
                } else {
                    // FAISS_BIN_IDMAP
                    if (metric_type == static_cast<int64_t>(MetricType::HAMMING) ||
                        metric_type == static_cast<int64_t>(MetricType::JACCARD) ||
                        metric_type == static_cast<int64_t>(MetricType::TANIMOTO) ||
                        metric_type == static_cast<int64_t>(MetricType::SUBSTRUCTURE) ||
                        metric_type == static_cast<int64_t>(MetricType::SUPERSTRUCTURE)) {
                        // do nothing
                    } else {
                        Illegal_Metric_Type();
                        return;
                    }
------}

--// step 2: search
--bool hybrid = std::dynamic_pointer_cast<SpecResLabel>(label_)->IsHybrid();
--if (!vectors.float_data_.empty()) {
----s = index_engine_->Search(nq, vectors.float_data_.data(), topk, extra_params, output_distance.data(),output_ids.data(), hybrid);
------ExecutionEngineImpl::Search
--else if (!vectors.binary_data_.empty()) {
----s = index_engine_->Search(nq, vectors.binary_data_.data(), topk, extra_params, output_distance.data(),output_ids.data(), hybrid);
--}

--// step 3: pick up topk result
--XSearchTask::MergeTopkToResultSet(output_ids, output_distance, spec_k, nq, topk, ascending_reduce,
                                                  search_job->GetResultIds(), search_job->GetResultDistances());

```