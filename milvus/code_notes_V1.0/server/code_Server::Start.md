#1.Server::Start

```
Server::Start
--Daemonize
--LoadConfig
----config = Config::GetInstance();
----config.LoadConfigFile(config_filename_);
----config.ValidateConfig
--config = Config::GetInstance();
--boost::filesystem::create_directories(db_path);
--InstanceLockCheck::Check(db_path);
--if (wal_enable)
----boost::filesystem::create_directories(wal_path);
---- InstanceLockCheck::Check(wal_path);
--/* record config and hardware information into log */
--LogConfigInFile(config_filename_);
--LogCpuInfo();
--LogConfigInMem();
--server::Metrics::GetInstance().Init();
--server::SystemInfo::GetInstance().Init();
----SystemInfo::Init
--StartService
```