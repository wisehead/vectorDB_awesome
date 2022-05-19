#1.NewRootCoord

```
NewRootCoord
--rc.NewServer(ctx, factory)
----s := &Server{
		ctx:         ctx1,
		cancel:      cancel,
		grpcErrChan: make(chan error),
	}
----s.setClient()
----s.rootCoord, err = rootcoord.NewCore(s.ctx, factory)
------NewCore
--------core := &Core{
		ctx:     ctx,
		cancel:  cancel,
		ddlLock: sync.Mutex{},
		factory: factory,
	    }
--return &RootCoord{
		ctx: ctx,
		svr: svr,
	}
```