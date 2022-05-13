#1.struct GeneralQuery

```cpp
struct GeneralQuery {
    LeafQueryPtr leaf;
    BinaryQueryPtr bin = std::make_shared<BinaryQuery>();
};
```

#2.struct LeafQuery

```cpp
struct LeafQuery {
    TermQueryPtr term_query;
    RangeQueryPtr range_query;
    VectorQueryPtr vector_query;
    float query_boost;
};

```

#3.struct BinaryQuery

```cpp
struct BinaryQuery {
    GeneralQueryPtr left_query;
    GeneralQueryPtr right_query;
    QueryRelation relation;
    float query_boost;
};
```