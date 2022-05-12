#1.class MySQLMetaImpl

```cpp
class MySQLMetaImpl : public Meta {

 private:
    const DBMetaOptions options_;
    const int mode_;

    std::shared_ptr<MySQLConnectionPool> mysql_connection_pool_;
    bool safe_grab_ = false;  // Safely graps a connection from mysql pool

    std::mutex meta_mutex_;
    std::mutex genid_mutex_;
    //        std::mutex connectionMutex_;
};  // DBMetaImpl
```