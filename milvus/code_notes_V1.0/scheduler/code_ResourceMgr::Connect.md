#1.ResourceMgr::Connect

```
ResourceMgr::Connect
--auto res1 = GetResource(name1);
--auto res2 = GetResource(name2);
--if (res1 && res2)
----res1->AddNeighbour(std::static_pointer_cast<Node>(res2), connection);
```

#2.caller

```cpp
void
load_simple_config() {
    // create and connect
    ResMgrInst::GetInstance()->Add(ResourceFactory::Create("disk", "DISK", 0, false));

    auto io = Connection("io", 500);
    ResMgrInst::GetInstance()->Add(ResourceFactory::Create("cpu", "CPU", 0));
    ResMgrInst::GetInstance()->Connect("disk", "cpu", io);
}    
```