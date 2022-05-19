#1.MilvusRoles.runRootCoord

```
MilvusRoles.runRootCoord
--wg.Add(1)
--go func()
----rootcoord.Params.InitOnce()
----if localMsg {
------rootcoord.Params.SetLogConfig(typeutil.StandaloneRole)
----else {
------rootcoord.Params.SetLogConfig(typeutil.RootCoordRole)
----factory := dependency.NewFactory(localMsg)
----rc, err = components.NewRootCoord(ctx, factory)
------svr, err := rc.NewServer(ctx, factory)
----if !localMsg {
------http.Handle(healthz.HealthzRouterPath, &componentsHealthzHandler{component: rc})
----wg.Done()
----_ = rc.Run()
------RootCoord.Run
--------rc.svr.Run()
--wg.Wait()
--metrics.RegisterRootCoord(Registry)
```