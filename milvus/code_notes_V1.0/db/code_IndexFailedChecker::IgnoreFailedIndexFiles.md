#1.IndexFailedChecker::IgnoreFailedIndexFiles

```
IndexFailedChecker::IgnoreFailedIndexFiles
--// there could be some failed files belong to different collection.
  // some files may has failed for several times, no need to build index for these files.
  // thus we can avoid dead circle for build index operation
--for (auto it_file = table_files.begin(); it_file != table_files.end();) {
----auto it_failed_files = index_failed_files_.find((*it_file).collection_id_);
----if (it_failed_files != index_failed_files_.end()) {
------auto it_failed_file = it_failed_files->second.find((*it_file).file_id_);
------if (it_failed_file != it_failed_files->second.end()) {
--------if (it_failed_file->second.size() >= INDEX_FAILED_RETRY_TIME) {
----------it_file = table_files.erase(it_file);
----------continue;
                }
            }
        }

        ++it_file;
    }
```