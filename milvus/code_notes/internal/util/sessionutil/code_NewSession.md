#1.NewSession

```
NewSession
--session := &Session{
		ctx:      ctx,
		metaRoot: metaRoot,
	}
--session.UpdateRegistered(false)	
--err := retry.Do(ctx, connectEtcdFn, retry.Attempts(100))
```

#2. connectEtcdFn

```go
connectEtcdFn := func() error {
		log.Debug("Session try to connect to etcd")
		ctx2, cancel2 := context.WithTimeout(session.ctx, 5*time.Second)
		defer cancel2()
		if _, err := client.Get(ctx2, "health"); err != nil {
			return err
		}
		session.etcdCli = client
		return nil
	}
```