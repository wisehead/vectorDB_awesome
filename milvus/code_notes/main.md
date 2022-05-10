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
--InstanceLockCheck::Release
----fd = open(InstanceLockCheck::GetInstance()->lk_path.c_str(), O_RDWR | O_CREAT | O_NOFOLLOW, 0640);
----close(fd);
--Server::Init
----daemonized_ = daemonized;
----pid_filename_ = pid_filename;
----config_filename_ = config_filename;
--Server::Start
--/* wait signal */
--pause();
```