#1.XBuildIndexTask::Load

```
XBuildIndexTask::Load
--if (auto job = job_.lock())
----auto build_index_job = std::static_pointer_cast<scheduler::BuildIndexJob>(job);
----auto options = build_index_job->options();
```