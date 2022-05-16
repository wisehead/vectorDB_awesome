#1.DBImpl::ExecWalRecord

```
DBImpl::ExecWalRecord
--lambda collections_flushed
--switch (record.type) 
----case wal::MXLogType::Entity:
------status = GetPartitionByTag(record.collection_id, record.partition_tag, target_collection_name);
------status = mem_mgr_->InsertEntities(
                target_collection_name, record.length, record.ids, (record.data_size / record.length / sizeof(float)),
                (const float*)record.data, record.attr_nbytes, record.attr_data_size, record.attr_data, record.lsn);
--------MemManagerImpl::InsertEntities                
------force_flush_if_mem_full();
--------InternalFlush

----case wal::MXLogType::InsertBinary:
------status = GetPartitionByTag(record.collection_id, record.partition_tag, target_collection_name);
------status = mem_mgr_->InsertVectors(target_collection_name, record.length, record.ids,
                                             (record.data_size / record.length / sizeof(uint8_t)),
                                             (const u_int8_t*)record.data, record.lsn);
------force_flush_if_mem_full

----case wal::MXLogType::InsertVector:
------status = GetPartitionByTag(record.collection_id, record.partition_tag, target_collection_name);
------status = mem_mgr_->InsertVectors(target_collection_name, record.length, record.ids,
                                             (record.data_size / record.length / sizeof(float)),
                                             (const float*)record.data, record.lsn);

----case wal::MXLogType::Delete:
------std::vector<meta::CollectionSchema> partition_array;
------status = meta_ptr_->ShowPartitions(record.collection_id, partition_array);
------if (record.length == 1) {
                for (auto& collection_id : collection_ids) {
                    status = mem_mgr_->DeleteVector(collection_id, *record.ids, record.lsn);
                    if (!status.ok()) {
                        return status;
                    }
                }
-=-----} else {
                for (auto& collection_id : collection_ids) {
                    status = mem_mgr_->DeleteVectors(collection_id, record.length, record.ids, record.lsn);
                    if (!status.ok()) {
                        return status;
                    }
                }
            }
```

#2.lambda collections_flushed

```
lambda collections_flushed
--for (auto& collection : target_collection_names)
----meta_ptr_->GetCollectionFlushLSN(collection, lsn);
------statement << "SELECT flush_lsn FROM " << META_TABLES << " WHERE table_id = " << mysqlpp::quote << collection_id << ";";
--wal_mgr_->CollectionFlushed(collection_id, lsn);
----auto it_col = collections_.find(collection_id);
----if (it_col != collections_.end())
------for (auto& part : it_col->second) {
--------part.second.flush_lsn = lsn;
--std::set<std::string> merge_collection_ids;
--for (auto& collection : target_collection_names) {
----merge_collection_ids.insert(collection);
--StartMergeTask(merge_collection_ids);
--return max_lsn;
```

#3.force_flush_if_mem_full

```
force_flush_if_mem_full
--if (mem_mgr_->GetCurrentMem() > options_.insert_buffer_size_) 
----MemManagerImpl::GetCurrentMem
------GetCurrentMutableMem() + GetCurrentImmutableMem();
--------MemManagerImpl::GetCurrentMutableMem
----------for (auto& kv : mem_id_map_) {
------------auto memTable = kv.second;
------------total_mem += memTable->GetCurrentMem();
--------------MemTable::GetCurrentMem
----------------for (auto& mem_table_file : mem_table_file_list_) {
------------------total_mem += mem_table_file->GetCurrentMem();
--------------------MemTableFile::GetCurrentMem
--------MemManagerImpl::GetCurrentImmutableMem
----------for (auto& mem_table : immu_mem_list_) {
------------total_mem += mem_table->GetCurrentMem();
--------------MemTable::GetCurrentMem
----------------for (auto& mem_table_file : mem_table_file_list_) {
------------------total_mem += mem_table_file->GetCurrentMem();
--------------------MemTableFile::GetCurrentMem
----InternalFlush();
------DBImpl::InternalFlush
--------record.type = wal::MXLogType::Flush;
--------record.collection_id = collection_id;
--------ExecWalRecord(record);
----------DBImpl::ExecWalRecord
```