#1.main

```
main
--server = milvus::server::Server::GetInstance();
--getopt_long
--/* Handle Signal */                                        
--signal(SIGHUP, milvus::server::SignalUtil::HandleSignal);  
--signal(SIGINT, milvus::server::SignalUtil::HandleSignal);  
--signal(SIGUSR1, milvus::server::SignalUtil::HandleSignal); 
--signal(SIGSEGV, milvus::server::SignalUtil::HandleSignal); 
--signal(SIGUSR2, milvus::server::SignalUtil::HandleSignal); 
--signal(SIGTERM, milvus::server::SignalUtil::HandleSignal); 

```