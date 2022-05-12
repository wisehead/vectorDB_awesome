#1.XBuildIndexTask::Execute

```
XBuildIndexTask::Execute
--job = job_.lock()//weak_ptr -> shared_ptr
--auto build_index_job = std::static_pointer_cast<scheduler::BuildIndexJob>(job);
```