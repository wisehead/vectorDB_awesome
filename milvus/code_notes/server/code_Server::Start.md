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
--
```