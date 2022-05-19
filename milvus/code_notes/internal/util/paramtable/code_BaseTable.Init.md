#1.BaseTable.Init

```
BaseTable.Init
--gp.params = memkv.NewMemoryKV()
--gp.configDir = gp.initConfPath()
--gp.loadFromYaml(defaultYaml)
--gp.tryLoadFromEnv()
--gp.InitLogCfg()
```

#2.NewMemoryKV

```go
// NewMemoryKV returns an in-memory kvBase for testing.
func NewMemoryKV() *MemoryKV {
	return &MemoryKV{
		tree: btree.New(2),
	}
}
```

#3.func (gp *BaseTable) initConfPath() string

```
func (gp *BaseTable) initConfPath() string
--// check if user set conf dir through env
--configDir, find := syscall.Getenv("MILVUSCONF")
--if !find
----runPath, err := os.Getwd()
----configDir = runPath + "/configs/"
----if _, err := os.Stat(configDir); err != nil
------_, fpath, _, _ := runtime.Caller(0)
------configDir = path.Dir(fpath) + "/../../../configs/"
--return configDir
```

#4.func (gp *BaseTable) loadFromYaml(file string)

```
func (gp *BaseTable) loadFromYaml(file string)
--gp.LoadYaml(file)
```

#5.gp.LoadYaml(file)

```

```