#1.class LRU

```cpp
template <typename key_t, typename value_t>
class LRU {
 public:
    typedef typename std::pair<key_t, value_t> key_value_pair_t;
    typedef typename std::list<key_value_pair_t>::iterator list_iterator_t;
    typedef typename std::list<key_value_pair_t>::reverse_iterator reverse_list_iterator_t;

 private:
    std::list<key_value_pair_t> cache_items_list_;
    std::unordered_map<key_t, list_iterator_t> cache_items_map_;
    size_t max_size_;
    list_iterator_t iter_;
};

```