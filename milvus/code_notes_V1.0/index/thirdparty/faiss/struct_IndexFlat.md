#1.struct IndexFlat

```cpp
/** Index that stores the full vectors and performs exhaustive search */
struct IndexFlat: Index {

    /// database vectors, size ntotal * d
    std::vector<float> xb;

};

```