#1.FilesHolder::UnmarkFileInternal

```
FilesHolder::UnmarkFileInternal
--if (unique_ids_.find(file.id_) == unique_ids_.end()) {
        return Status::OK();  // no such file
--}
--auto status = OngoingFileChecker::GetInstance().UnmarkOngoingFile(file);
----FilesHolder::OngoingFileChecker::UnmarkOngoingFile
------FilesHolder::OngoingFileChecker::UnmarkOngoingFileNoLock

```