#1.class HierarchicalNSW

```cpp
template<typename dist_t>
class HierarchicalNSW : public AlgorithmInterface<dist_t> {
    // linxj: use for free resource
    SpaceInterface<dist_t> *space;
    size_t metric_type_; // 0:l2, 1:ip

    size_t max_elements_;
    size_t cur_element_count;
    size_t size_data_per_element_;
    size_t size_links_per_element_;

    size_t M_;
    size_t maxM_;
    size_t maxM0_;
    size_t ef_construction_;

    double mult_;
    int maxlevel_;


    VisitedListPool *visited_list_pool_;
    std::mutex cur_element_count_guard_;

    std::vector<std::mutex> link_list_locks_;
    tableint enterpoint_node_;


    size_t size_links_level0_;
    size_t offsetData_, offsetLevel0_;


    char *data_level0_memory_;
    char **linkLists_;
    std::vector<int> element_levels_;

    size_t data_size_;

    bool has_deletions_;


    size_t label_offset_;
    DISTFUNC<dist_t> fstdistfunc_;
    void *dist_func_param_;
    std::unordered_map<labeltype, tableint> label_lookup_;

    std::default_random_engine level_generator_;
}    
```