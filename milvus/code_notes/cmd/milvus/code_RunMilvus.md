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
--// Setup logger in advance for standalone and embedded Milvus.
  // Any log from this point on is under control.
--if serverType == typeutil.StandaloneRole || serverType == typeutil.EmbeddedRole {
		var params paramtable.BaseTable
		if serverType == typeutil.EmbeddedRole {
			params.GlobalInitWithYaml("embedded-milvus.yaml")
		} else {
			params.Init()
		}
		params.SetLogConfig()
		params.RoleName = serverType
		params.SetLogger(0)
	}
--runtimeDir := createRuntimeDir(serverType)
--filename := getPidFileName(serverType, svrAlias)
--case "run":
		printBanner(flags.Output())
		injectVariablesToEnv()
		lock, err := createPidFile(flags.Output(), filename, runtimeDir)
		if err != nil {
			panic(err)
		}
		defer removePidFile(lock)
		role.Run(local, svrAlias)
		--(mr *MilvusRoles) Run
	case "stop":
		if err := stopPid(filename, runtimeDir); err != nil {
			fmt.Fprintf(os.Stderr, "%s\n\n", err.Error())
		}
	case "dry-run":
		// A dry run does not actually bring up the Milvus instance.
	default:
		fmt.Fprintf(os.Stderr, "unknown command : %s\n", command)
	}
```