#1.Resource::Start

```
Resource::Start
--running_ = true;
--loader_thread_ = std::thread(&Resource::loader_function, this);
--executor_thread_ = std::thread(&Resource::executor_function, this);
```

#2.Resource::loader_function

```
Resource::loader_function
--
```