#1.SignalUtil::HandleSignal

```
SignalUtil::HandleSignal
--InstanceLockCheck::Release
--switch (signum) {
        case SIGINT:
        case SIGUSR2: {
            LOG_SERVER_INFO_ << "Server received signal: " << signum;

            server::Server& server = server::Server::GetInstance();
            server.Stop();

            exit(0);
        }
        default: {
            LOG_SERVER_INFO_ << "Server received critical signal: " << signum;
            SignalUtil::PrintStacktrace();

            server::Server& server = server::Server::GetInstance();
            server.Stop();

            exit(1);
        }
    }
```