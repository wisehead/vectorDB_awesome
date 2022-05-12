#1.class BasicVectorSet

```cpp
class BasicVectorSet : public VectorSet
{
private:
    ByteArray m_data;

    VectorValueType m_valueType;

    DimensionType m_dimension;

    SizeType m_vectorCount;

    SizeType m_perVectorDataSize;
};
```