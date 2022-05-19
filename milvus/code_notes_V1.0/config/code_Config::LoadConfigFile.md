#1.Config::LoadConfigFile

```
Config::LoadConfigFile
--ConfigMgr* mgr = YamlConfigMgr::GetInstance();
--STATUS_CHECK(mgr->LoadConfigFile(filename));
----YamlConfigMgr::LoadConfigFile
------node_ = YAML::LoadFile(filename);
------YamlConfigMgr::LoadConfigNode(node_, config_);
--------for (YAML::const_iterator it = node.begin(); it != node.end(); ++it) {
        	if (!it->first.IsNull()) {
          	  key = it->first.as<std::string>();
        	}
        	if (node[key].IsScalar()) {
          	  SetConfigValue(node, key, config);
        	} else if (node[key].IsMap()) {
          	  SetChildConfig(node, key, config);
        	} else if (node[key].IsSequence()) {
          	  SetSequence(node, key, config);
        	}
    	 }
```