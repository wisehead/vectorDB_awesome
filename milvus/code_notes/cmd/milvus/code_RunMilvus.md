#1.milvus.RunMilvus

```go
RunMilvus
--command := args[1]
  serverType := args[2]
  flags := flag.NewFlagSet(args[0], flag.ExitOnError)
--flags.StringVar(&svrAlias, "alias", "", "set alias")
--flags.BoolVar(&enableRootCoord, typeutil.RootCoordRole, false, "enable root coordinator")
	flags.BoolVar(&enableQueryCoord, typeutil.QueryCoordRole, false, "enable query coordinator")
	flags.BoolVar(&enableIndexCoord, typeutil.IndexCoordRole, false, "enable index coordinator")
	flags.BoolVar(&enableDataCoord, typeutil.DataCoordRole, false, "enable data coordinator")
--// Discard Milvus welcome logs, init logs and maxprocs logs in embedded Milvus.
--if serverType == typeutil.EmbeddedRole {
		flags.SetOutput(io.Discard)
		// Initialize maxprocs while discarding log.
		maxprocs.Set(maxprocs.Logger(nil))
--} else {
		// Initialize maxprocs.
		maxprocs.Set(maxprocs.Logger(syslog.Printf))
--}
```