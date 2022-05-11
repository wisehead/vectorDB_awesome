#1.class AnnoyIndexInterface

```cpp
template<typename S, typename T>
class AnnoyIndexInterface {
 public:
  // Note that the methods with an **error argument will allocate memory and write the pointer to that string if error is non-nullptr
  virtual ~AnnoyIndexInterface() {};
  virtual bool add_item(S item, const T* w, char** error=nullptr) = 0;
  virtual bool build(int q, char** error=nullptr) = 0;
  virtual bool unbuild(char** error=nullptr) = 0;
  virtual bool save(const char* filename, bool prefault=false, char** error=nullptr) = 0;
  virtual void unload() = 0;
  virtual bool load(const char* filename, bool prefault=false, char** error=nullptr) = 0;
  virtual bool load_index(void* index_data, const int64_t& index_size, char** error = nullptr) = 0;
  virtual T get_distance(S i, S j) const = 0;
  virtual void get_nns_by_item(S item, size_t n, int64_t search_k, vector<S>* result, vector<T>* distances,
                               faiss::ConcurrentBitsetPtr& bitset = nullptr) const = 0;
  virtual void get_nns_by_vector(const T* w, size_t n, int64_t search_k, vector<S>* result, vector<T>* distances,
                               faiss::ConcurrentBitsetPtr& bitset = nullptr) const = 0;
  virtual S get_n_items() const = 0;
  virtual S get_dim() const = 0;
  virtual S get_n_trees() const = 0;
  virtual int64_t get_index_length() const = 0;
  virtual void* get_index() const = 0;
  virtual void verbose(bool v) = 0;
  virtual void get_item(S item, T* v) const = 0;
  virtual void set_seed(int q) = 0;
  virtual bool on_disk_build(const char* filename, char** error=nullptr) = 0;
  virtual int64_t cal_size() = 0;
};
```

