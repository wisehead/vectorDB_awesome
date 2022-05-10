#1.Server::Start

```
Server::Start
--Daemonize
--LoadConfig
----config = Config::GetInstance();
----config.LoadConfigFile(config_filename_);
----config.ValidateConfig
--config = Config::GetInstance();
```