#1.class Job

```cpp
class Job : public interface::dumpable {
 public:
    inline JobId
    id() const {
        return id_;
    }

    inline JobType
    type() const {
        return type_;
    }

    json
    Dump() const override;

 protected:
    explicit Job(JobType type);

 private:
    JobId id_ = 0;
    JobType type_;
};
```

#2.enum JobType
```cpp
enum class JobType {
    INVALID,
    SEARCH,
    DELETE,
    BUILD,
};

using JobId = std::uint64_t;
```