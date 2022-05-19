#1.JobMgr::calculate_path

```
JobMgr::calculate_path
--std::vector<std::string> path;
--auto spec_label = std::static_pointer_cast<SpecResLabel>(task->label());
--auto src = res_mgr->GetDiskResources()[0];
--auto dest = spec_label->resource();
--ShortestPath(src.lock(), dest.lock(), res_mgr, path);
--task->path() = Path(path, path.size() - 1);
```