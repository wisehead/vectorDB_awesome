#1.TaskCreator::Create

```
TaskCreator::Create
--switch (job->type())
----case JobType::SEARCH: 
------Create(std::static_pointer_cast<SearchJob>(job));
----case JobType::DELETE: {
------return Create(std::static_pointer_cast<DeleteJob>(job));
----case JobType::BUILD: {
------return Create(std::static_pointer_cast<BuildIndexJob>(job));
----default: {
------return std::vector<TaskPtr>();
```


#2.TaskCreator::Create

```cpp
TaskCreator::Create(const BuildIndexJobPtr& job)
--for (auto& to_index_file : job->to_index_files())
----auto task = std::make_shared<XBuildIndexTask>(to_index_file.second, nullptr);
----task->job_ = job;
----tasks.emplace_back(task);
}
```

