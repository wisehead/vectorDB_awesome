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