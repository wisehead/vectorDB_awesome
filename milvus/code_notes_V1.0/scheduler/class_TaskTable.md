#1.class TaskTable

```cpp
class TaskTable : public interface::dumpable {
 private:
    std::uint64_t id_ = 0;
    CircleQueue<TaskTableItemPtr> table_;
    std::function<void(void)> subscriber_ = nullptr;

    // cache last finish avoid Pick task from begin always
    // pick from (last_finish_ + 1)
    // init with -1, pick from (last_finish_ + 1) = 0
    uint64_t last_finish_ = -1;
};

```

#2.struct TaskTableItem

```cpp
struct TaskTableItem;
using TaskTableItemPtr = std::shared_ptr<TaskTableItem>;

struct TaskTableItem : public interface::dumpable {
    uint64_t id;               // auto increment from 0;
    TaskTableItemState state;  // the state;
    std::mutex mutex;
    TaskTimestamp timestamp;
    TaskTableItemPtr from;

 private:
    TaskPtr task;  // the task;
};

```

#3. TaskTableItemState and TaskTimestamp

```cpp
enum class TaskTableItemState {
    INVALID,
    START,      // idle
    LOADING,    // loading data from other resource
    LOADED,     // ready to exec or move
    EXECUTING,  // executing, locking util executed or failed
    EXECUTED,   // executed, termination state
    MOVING,     // moving to another resource, locking util executed or failed
    MOVED,      // moved, termination state
};

struct TaskTimestamp : public interface::dumpable {
    uint64_t start = 0;
    uint64_t move = 0;
    uint64_t moved = 0;
    uint64_t load = 0;
    uint64_t loaded = 0;
    uint64_t execute = 0;
    uint64_t executed = 0;
    uint64_t finish = 0;

    json
    Dump() const override;
};

```