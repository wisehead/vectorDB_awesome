#1.class AlgorithmInterface

```cpp
    template<typename dist_t>
    class AlgorithmInterface {
    public:
        virtual void addPoint(const void *datapoint, labeltype label)=0;
        virtual std::priority_queue<std::pair<dist_t, labeltype >> searchKnn(const void *, size_t, faiss::ConcurrentBitsetPtr bitset) const = 0;
        template <typename Comp>
        std::vector<std::pair<dist_t, labeltype>> searchKnn(const void*, size_t, Comp, faiss::ConcurrentBitsetPtr bitset) {
        }
        virtual void saveIndex(const std::string &location)=0;
        virtual ~AlgorithmInterface(){
        }
    };
```