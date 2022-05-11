#1.clas Task 

```
class Task {

 public:
    Path task_path_;
    scheduler::JobWPtr job_;
    TaskType type_;
    TaskLabelPtr label_ = nullptr;
};
```
