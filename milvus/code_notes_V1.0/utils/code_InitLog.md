#1.InitLog

```
InitLog
--el::Configurations defaultConf;
    defaultConf.setToDefault();
    defaultConf.setGlobally(el::ConfigurationType::Format, "[%datetime][%level]%msg");
    defaultConf.setGlobally(el::ConfigurationType::ToFile, boolen_to_string(log_to_file));
    defaultConf.setGlobally(el::ConfigurationType::ToStandardOutput, boolen_to_string(log_to_stdout));
    defaultConf.setGlobally(el::ConfigurationType::SubsecondPrecision, "3");
    defaultConf.setGlobally(el::ConfigurationType::PerformanceTracking, str_false);
--defaultConf.setGlobally(el::ConfigurationType::MaxLogFileSize, std::to_string(max_log_file_size));
    el::Loggers::addFlag(el::LoggingFlag::StrictLogFileSizeCheck);
    el::Helpers::installPreRollOutCallback(RolloutHandler);
    el::Loggers::addFlag(el::LoggingFlag::DisableApplicationAbortOnFatalLog);
--el::Loggers::reconfigureLogger("default", defaultConf);    
```