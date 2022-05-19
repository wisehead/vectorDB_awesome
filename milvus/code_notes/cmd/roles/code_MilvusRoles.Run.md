#1.(mr *MilvusRoles) Run

```
(mr *MilvusRoles) Run
--ctx, cancel := context.WithCancel(context.Background())
--if local
----os.Setenv(metricsinfo.DeployModeEnvKey, metricsinfo.StandaloneDeployMode)
----Params.Init()
----if Params.RocksmqEnable() {
------path, _ := Params.Load("_RocksmqPath")
------err := rocksmqimpl.InitRocksMQ(path)
----if Params.EtcdCfg.UseEmbedEtcd {
------// Start etcd server.
------etcd.InitEtcdServer(&Params.EtcdCfg)
--else
----os.Setenv(metricsinfo.DeployModeEnvKey, metricsinfo.ClusterDeployMode)
--rc = mr.runRootCoord(ctx, local)
--pn = mr.runProxy(pctx, local, alias)
--qs = mr.runQueryCoord(ctx, local)
--qn = mr.runQueryNode(ctx, local, alias)
--ds = mr.runDataCoord(ctx, local)
--dn = mr.runDataNode(ctx, local, alias)
--is = mr.runIndexCoord(ctx, local)
--in = mr.runIndexNode(ctx, local, alias)
```