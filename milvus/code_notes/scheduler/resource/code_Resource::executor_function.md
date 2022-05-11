#1.Resource::executor_function

```
Resource::executor_function
--if (subscriber_) {
----auto event = std::make_shared<StartUpEvent>(shared_from_this());
----subscriber_(std::static_pointer_cast<Event>(event));
--while (running_) 
----while (true)
------Process(task_item->get_task());
```