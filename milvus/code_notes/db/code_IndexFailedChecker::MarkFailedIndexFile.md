#1.IndexFailedChecker::MarkFailedIndexFile

```cpp
IndexFailedChecker::MarkFailedIndexFile

auto iter = index_failed_files_.find(file.collection_id_);
    if (iter == index_failed_files_.end()) {
        File2ErrArray failed_files;
        failed_files.insert(std::make_pair(file.file_id_, std::vector<std::string>(1, err_msg)));
        index_failed_files_.insert(std::make_pair(file.collection_id_, failed_files));
    } else {
        auto it_failed_files = iter->second.find(file.file_id_);
        if (it_failed_files != iter->second.end()) {
            it_failed_files->second.push_back(err_msg);
        } else {
            iter->second.insert(std::make_pair(file.file_id_, std::vector<std::string>(1, err_msg)));
        }
    }

```