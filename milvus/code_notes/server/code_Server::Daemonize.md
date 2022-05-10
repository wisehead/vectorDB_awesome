#1.Server::Daemonize

```
//see this wiki: https://blog.csdn.net/mijichui2153/article/details/81394387
Server::Daemonize
--pid = fork();// Fork off the parent process
...
...
--std::string pid_file_context = std::to_string(getpid());
--ssize_t res = write(pid_fd_, pid_file_context.c_str(), pid_file_context.size());
```