#1.OptimizerInst::GetInstance


```
OptimizerInst::GetInstance
--std::vector<PassPtr> pass_list;
--pass_list.push_back(std::make_shared<FallbackPass>());
--instance = std::make_shared<Optimizer>(pass_list);
```