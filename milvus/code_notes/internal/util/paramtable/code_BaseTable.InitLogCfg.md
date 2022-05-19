#1.BaseTable.InitLogCfg

```
BaseTable.InitLogCfg
--gp.Log = log.Config{}
--format, err := gp.Load("log.format")

--gp.Log.Format = format
--level, err := gp.Load("log.level")

--gp.Log.Level = level
--gp.Log.File.MaxSize = gp.ParseInt("log.file.maxSize")
--gp.Log.File.MaxBackups = gp.ParseInt("log.file.maxBackups")
--gp.Log.File.MaxDays = gp.ParseInt("log.file.maxAge")
```