#1.GrpcServer::StartService

```
GrpcServer::StartService
--config.GetNetworkConfigBindAddress(address)
--config.GetNetworkConfigBindPort(port)
--std::string server_address(address + ":" + port);
--::grpc::ServerBuilder builder;
--builder.SetOption(std::unique_ptr<::grpc::ServerBuilderOption>(new NoReusePortOption));   
--builder.SetMaxReceiveMessageSize(MESSAGE_SIZE);  // default 4 * 1024 * 1024               
--builder.SetMaxSendMessageSize(MESSAGE_SIZE);                                              
                                                                                        
--builder.SetCompressionAlgorithmSupportStatus(GRPC_COMPRESS_STREAM_GZIP, true);            
--builder.SetDefaultCompressionAlgorithm(GRPC_COMPRESS_STREAM_GZIP);                        
--builder.SetDefaultCompressionLevel(GRPC_COMPRESS_LEVEL_NONE);                             
                                                                                          
--GrpcRequestHandler service(opentracing::Tracer::Global());                                
--service.RegisterRequestHandler(RequestHandler());                                         
                                                                                          
--builder.AddListeningPort(server_address, ::grpc::InsecureServerCredentials());            
--builder.RegisterService(&service);                                                        
                                                                                            
--GrpcRequestHandler service(opentracing::Tracer::Global());
--service.RegisterRequestHandler(RequestHandler());
----GrpcRequestHandler::RegisterRequestHandler
--builder.AddListeningPort(server_address, ::grpc::InsecureServerCredentials());
--builder.RegisterService(&service);
--// Add gRPC interceptor                                                                                             
--using InterceptorI = ::grpc::experimental::ServerInterceptorFactoryInterface;                                       
--using InterceptorIPtr = std::unique_ptr<InterceptorI>;                                                              
--std::vector<InterceptorIPtr> creators;                                                                                                                                                                                                
--creators.push_back(std::unique_ptr<::grpc::experimental::ServerInterceptorFactoryInterface>(new SpanInterceptorFactory(&service)));
--builder.experimental().SetInterceptorCreators(std::move(creators));
--server_ptr_ = builder.BuildAndStart();
--server_ptr_->Wait();
```