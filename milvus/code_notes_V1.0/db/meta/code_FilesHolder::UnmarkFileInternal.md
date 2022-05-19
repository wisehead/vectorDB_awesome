#1.FilesHolder::UnmarkFileInternal

```
FilesHolder::UnmarkFileInternal
--if (unique_ids_.find(file.id_) == unique_ids_.end()) {
        return Status::OK();  // no such file
--}
--auto status = OngoingFileChecker::GetInstance().UnmarkOngoingFile(file);
----FilesHolder::OngoingFileChecker::UnmarkOngoingFile
------FilesHolder::OngoingFileChecker::UnmarkOngoingFileNoLock
--for (auto iter = hold_files_.begin(); iter != hold_files_.end(); ++iter) 
----if (file.id_ == (*iter).id_)
------hold_files_.erase(iter);
--unique_ids_.erase(file.id_);
```