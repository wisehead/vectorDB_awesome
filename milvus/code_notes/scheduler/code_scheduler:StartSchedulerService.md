#1.scheduler::StartSchedulerService()

```
scheduler::StartSchedulerService()
--load_simple_config
--OptimizerInst::GetInstance()->Init();   
----Optimizer::Init() {
   	   for (auto& pass : pass_list_) {
        pass->Init();
      }
	 }  
--ResMgrInst::GetInstance()->Start();       
--SchedInst::GetInstance()->Start();        
--JobMgrInst::GetInstance()->Start();       
--CPUBuilderInst::GetInstance()->Start();   

```

#2.load_simple_config

```cpp
load_simple_config                                                              
--ResMgrInst::GetInstance()->Add(ResourceFactory::Create("disk", "DISK", 0, fals
----ResourceFactory::Create                                                     
----ResourceMgr::Add                                                            
------ResourceMgr::post_event                                                   
--------queue_.emplace(event);                                                  
--------event_cv_.notify_one();                                                 
------RegisterSubscriber                                                        
--------subscriber_ = std::move(subscriber);                                    
------switch (resource->type()) {                                               
      case ResourceType::DISK: {                                                
          disk_resources_.emplace_back(ResourceWPtr(resource));                 
          break;                                                                
      }                                                                         
      case ResourceType::CPU: {                                                 
          cpu_resources_.emplace_back(ResourceWPtr(resource));                  
          break;                                                                
      }                                                                         
      case ResourceType::GPU: {                                                 
          gpu_resources_.emplace_back(ResourceWPtr(resource));                  
          break;                                                                
      }                                                                         
      case ResourceType::FPGA: {                                                
          LOG_ENGINE_DEBUG_ << "add fpga resource";                             
          fpga_resources_.emplace_back(ResourceWPtr(resource));                 
          break;                                                                
      }                                                                         
      default: { break; }                                                       
  }                                                                             
  resources_.emplace_back(resource);                                            
--auto io = Connection("io", 500);                                              
--ResMgrInst::GetInstance()->Add(ResourceFactory::Create("cpu", "CPU", 0));     
--ResMgrInst::GetInstance()->Connect("disk", "cpu", io);                        
----ResourceMgr::Connect                                                        
------res1 = GetResource(name1);                                                
------res2 = GetResource(name2);                                                
------res1->AddNeighbour(std::static_pointer_cast<Node>(res2), connection);     
```