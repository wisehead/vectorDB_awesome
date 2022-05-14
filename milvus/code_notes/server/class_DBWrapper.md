#1.class DBWrapper

```cpp
class DBWrapper {
 private:
    DBWrapper() = default;
    ~DBWrapper() = default;

 public:
    static DBWrapper&
    GetInstance() {
        static DBWrapper wrapper;
        return wrapper;
    }

    static engine::DBPtr
    DB() {
        return GetInstance().EngineDB();
    }

    Status
    StartService();
    Status
    StopService();

    engine::DBPtr
    EngineDB() {
        return db_;
    }

 private:
    Status
    PreloadCollections(const std::string& preload_collections);

 private:
    engine::DBPtr db_;
};
```