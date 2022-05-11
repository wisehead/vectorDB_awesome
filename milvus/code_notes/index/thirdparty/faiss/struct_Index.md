#1.struct faiss::Index

```cpp
/** Abstract structure for an index, supports adding vectors and searching them.
 *
 * All vectors provided at add or search time are 32-bit float arrays,
 * although the internal representation may vary.
 */
struct Index {
    using idx_t = int64_t;  ///< all indices are this type
    using component_t = float;
    using distance_t = float;

    int d;                 ///< vector dimension
    idx_t ntotal;          ///< total nb of indexed vectors
    bool verbose;          ///< verbosity level

    /// set if the Index does not require training, or if training is
    /// done already
    bool is_trained;

    /// type of metric this index uses for search
    MetricType metric_type;
    float metric_arg;     ///< argument of the metric type


};

```