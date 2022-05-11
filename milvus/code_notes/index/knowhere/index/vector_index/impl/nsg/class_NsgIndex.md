#1.class NsgIndex

```cpp
class NsgIndex {
 public:
    enum Metric_Type {
        Metric_Type_L2,
        Metric_Type_IP,
    };

    size_t dimension;
    size_t ntotal;        // totabl nb of indexed vectors
    int32_t metric_type;  // enum Metric_Type
    Distance* distance_;

    float* ori_data_;
    int64_t* ids_;
    Graph nsg;   // final graph
    Graph knng;  // reset after build

    node_t navigation_point;  // offset of node in origin data

    bool is_trained = false;

    /*
     * build and search parameter
     */
    size_t search_length;
    size_t candidate_pool_size;  // search deepth in fullset
    size_t out_degree;
};


```