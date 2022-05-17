#1.DBWrapper::StartService

```
DBWrapper::StartService
--Config& config = Config::GetInstance();
--s = config.GetGeneralConfigMetaURI(opt.meta_.backend_uri_);
--config.GetStorageConfigPath(path);
--opt.meta_.path_ = path + "/db";
--config.GetStorageConfigAutoFlushInterval(opt.auto_flush_interval_);
--config.GetStorageConfigFileCleanupTimeup(opt.file_cleanup_timeout_);
--config.GetMetricConfigEnableMonitor(opt.metric_enable_);
--config.GetCacheConfigCacheInsertData(opt.insert_cache_immediately_);
--config.GetCacheConfigInsertBufferSize(insert_buffer_size);
--opt.insert_buffer_size_ = insert_buffer_size;
--bool cluster_enable = false;
    std::string cluster_role;
    STATUS_CHECK(config.GetClusterConfigEnable(cluster_enable));
    STATUS_CHECK(config.GetClusterConfigRole(cluster_role));
    if (not cluster_enable) {
        opt.mode_ = engine::DBOptions::MODE::SINGLE;
    } else if (cluster_role == "ro") {
        opt.mode_ = engine::DBOptions::MODE::CLUSTER_READONLY;
    } else if (cluster_role == "rw") {
        opt.mode_ = engine::DBOptions::MODE::CLUSTER_WRITABLE;
    } else {
        std::cerr << "Error: cluster.role is not one of rw and ro." << std::endl;
        kill(0, SIGUSR1);
    }
--config.GetWalConfigEnable(opt.wal_enable_);
--if (opt.wal_enable_) 
----config.GetWalConfigRecoveryErrorIgnore(opt.recovery_error_ignore_);
----config.GetWalConfigBufferSize(wal_buffer_size);
----wal_buffer_size /= (1024 * 1024);
----opt.buffer_size_ = wal_buffer_size;
----config.GetWalConfigWalPath(opt.mxlog_path_);
--config.GetEngineConfigOmpThreadNum(omp_thread);
--omp_set_num_threads(omp_thread);
--faiss::distance_compute_blas_threshold = use_blas_threshold;
--config.GetEngineConfigUseBlasThreshold(use_blas_threshold);
--config.GetDBConfigArchiveDiskThreshold(disk);
--if (disk > 0) {
        criterial[engine::ARCHIVE_CONF_DISK] = disk;
    }
--config.GetDBConfigArchiveDaysThreshold(days);
--opt.meta_.archive_conf_.SetCriterias(criterial);
--// create db root folder
    s = CommonUtil::CreateDirectory(opt.meta_.path_);
--for (auto& path : opt.meta_.slave_paths_) {
        s = CommonUtil::CreateDirectory(path);
    }
--db_ = engine::DBFactory::Build(opt);   
----DBFactory::Build
------return std::make_shared<DBImpl>(options);
--db_->Start();
----DBImpl::Start 
--s = config.GetCacheConfigPreloadCollection(preload_collections);
--s = PreloadCollections(preload_collections);
```