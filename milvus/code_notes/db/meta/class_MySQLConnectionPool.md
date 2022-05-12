#1.class MySQLConnectionPool

```cpp
class MySQLConnectionPool : public mysqlpp::ConnectionPool {
 public:
    // The object's only constructor
    MySQLConnectionPool(const std::string& dbName, const std::string& userName, const std::string& passWord,
                        const std::string& serverIp, int port = 0, int maxPoolSize = 8)
        : db_name_(dbName),
          user_(userName),
          password_(passWord),
          server_(serverIp),
          port_(port),
          max_pool_size_(maxPoolSize) {
    }

    // The destructor.  We _must_ call ConnectionPool::clear() here,
    // because our superclass can't do it for us.
    ~MySQLConnectionPool() override {
        clear();
    }

    mysqlpp::Connection*
    grab() override;

    // Other half of in-use conn count limit
    void
    release(const mysqlpp::Connection* pc) override;

    const std::string&
    db_name() const {
        return db_name_;
    }

 protected:
    // Superclass overrides
    mysqlpp::Connection*
    create() override;

    void
    destroy(mysqlpp::Connection* cp) override;

    unsigned int
    max_idle_time() override;

 private:
    // Number of connections currently in use
    std::atomic<int> conns_in_use_ = 0;

    // Our connection parameters
    std::string db_name_, user_, password_, server_;
    int port_;

    int max_pool_size_;

    unsigned int max_idle_time_ = 10;  // 10 seconds
};
```