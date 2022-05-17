#1.SearchCombineRequest::CanCombine

```
SearchCombineRequest::CanCombine
--if (left->CollectionName() != right->CollectionName()) {
        return false;
    }

--if (left->ExtraParams() != right->ExtraParams()) {
        return false;
    }
--// topk must within certain range
    if (abs(left->TopK() - right->TopK() > MAX_TOPK_GAP)) {
        return false;
    }

--// sum of nq must less-equal than MAX_NQ
    if (left->VectorsData().vector_count_ > max_nq || right->VectorsData().vector_count_ > max_nq) {
        return false;
    }
    
--uint64_t total_nq = left->VectorsData().vector_count_ + right->VectorsData().vector_count_;
    if (total_nq > max_nq) {
        return false;
    }
    
--// partition list must be equal for each one
    std::set<std::string> left_partition_list, right_partition_list;
    GetUniqueList(left->PartitionList(), left_partition_list);
    GetUniqueList(right->PartitionList(), right_partition_list);
    if (!IsSameList(left_partition_list, right_partition_list)) {
        return false;
    }
    
--// file id list must be equal for each one
    std::set<std::string> left_file_id_list, right_file_id_list;
    GetUniqueList(left->FileIDList(), left_file_id_list);
    GetUniqueList(right->FileIDList(), right_file_id_list);
    if (!IsSameList(left_file_id_list, right_file_id_list)) {
        return false;
    }                
```