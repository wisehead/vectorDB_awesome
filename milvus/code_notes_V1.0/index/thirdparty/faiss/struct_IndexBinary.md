#1.struct IndexBinary

```cpp
/** Abstract structure for a binary index.
 *
 * Supports adding vertices and searching them.
 *
 * All queries are symmetric because there is no distinction between codes and
 * vectors.
 */
struct IndexBinary {
  using idx_t = Index::idx_t;    ///< all indices are this type
  using component_t = uint8_t;
  using distance_t = int32_t;

  int d;                 ///< vector dimension
  int code_size;   ///< number of bytes per vector ( = d / 8 )
  idx_t ntotal;          ///< total nb of indexed vectors
  bool verbose;          ///< verbosity level

  /// set if the Index does not require training, or if training is done already
  bool is_trained;

  /// type of metric this index uses for search
  MetricType metric_type;
};

```