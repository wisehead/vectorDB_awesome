#1.RequestScheduler::PutToQueue

```
RequestScheduler::PutToQueue
--std::string group_name = request_ptr->RequestGroup();
--if (request_groups_.count(group_name) > 0) 
----request_groups_[group_name]->PutRequest(request_ptr);
------RequestQueue::PutRequest
--else {
        RequestQueuePtr queue = std::make_shared<RequestQueue>();
        queue->PutRequest(request_ptr);
        request_groups_.insert(std::make_pair(group_name, queue));
        fiu_do_on("RequestScheduler.PutToQueue.null_queue", queue = nullptr);

        // start a thread
        ThreadPtr thread = std::make_shared<std::thread>(&RequestScheduler::TakeToExecute, this, queue);

        fiu_do_on("RequestScheduler.PutToQueue.push_null_thread", execute_threads_.push_back(nullptr));
        execute_threads_.push_back(thread);
        LOG_SERVER_INFO_ << "Create new thread for request group: " << group_name;
    }
```