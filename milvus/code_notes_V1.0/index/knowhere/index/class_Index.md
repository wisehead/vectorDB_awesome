#1.class Index

```cpp
class Index : public milvus::cache::DataObj {
 public:
    virtual BinarySet
    Serialize(const Config& config = Config()) = 0;

    virtual void
    Load(const BinarySet&) = 0;
};
```