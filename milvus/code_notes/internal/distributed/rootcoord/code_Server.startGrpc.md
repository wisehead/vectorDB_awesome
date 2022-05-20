#1.Server.startGrpc

```
Server.startGrpc
--go s.startGrpcLoop(port)
```

#2. Server.startGrpcLoop

```
startGrpcLoop
--lis, err := net.Listen("tcp", ":"+strconv.Itoa(port))
--s.grpcServer = grpc.NewServer(
		grpc.KeepaliveEnforcementPolicy(kaep),
		grpc.KeepaliveParams(kasp),
		grpc.MaxRecvMsgSize(Params.ServerMaxRecvSize),
		grpc.MaxSendMsgSize(Params.ServerMaxSendSize),
		grpc.UnaryInterceptor(ot.UnaryServerInterceptor(opts...)),
		grpc.StreamInterceptor(ot.StreamServerInterceptor(opts...)))
----grpc.NewServer//lib
--rootcoordpb.RegisterRootCoordServer(s.grpcServer, s)
----s.RegisterService(&_RootCoord_serviceDesc, srv)
------Server.RegisterService//lib
--go funcutil.CheckGrpcReady(ctx, s.grpcErrChan)
--err := s.grpcServer.Serve(lis);		
```