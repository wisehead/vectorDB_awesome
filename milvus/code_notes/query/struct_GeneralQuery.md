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

#4.struct TermQuery

```cpp
struct TermQuery {
    std::string field_name;
    std::vector<uint8_t> field_value;
    float boost;
};
```

#5.struct RangeQuery
```cpp
struct RangeQuery {
    std::string field_name;
    std::vector<CompareExpr> compare_expr;
    float boost;
};
```

#6.struct VectorQuery 

```cpp
struct VectorQuery {
    std::string field_name;
    milvus::json extra_params;
    int64_t topk;
    float boost;
    VectorRecord query_vector;
};
```

#7.struct VectorRecord

```cpp
struct VectorRecord {
    std::vector<float> float_data;
    std::vector<uint8_t> binary_data;
};
```

#8.enum class QueryRelation

```
enum class QueryRelation {
    INVALID = 0,
    R1,
    R2,
    R3,
    R4,
    AND,
    OR,
};
```

#9.struct CompareExpr

```cpp
struct CompareExpr {
    CompareOperator compare_operator;
    std::string operand;
};

```

#10.enum class CompareOperator

```cpp
enum class CompareOperator {
    LT = 0,
    LTE,
    EQ,
    GT,
    GTE,
    NE,
};
```