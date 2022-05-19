#1.BaseTable.LoadYaml

```
BaseTable.LoadYaml
--config := viper.New()
--configFile := gp.configDir + fileName
--os.Stat(configFile)
--config.SetConfigFile(configFile)
--config.ReadInConfig()
--for _, key := range config.AllKeys() {
		val := config.Get(key)
		str, err := cast.ToStringE(val)
		if err != nil {
			switch val := val.(type) {
			case []interface{}:
				str = str[:0]
				for _, v := range val {
					ss, err := cast.ToStringE(v)
					if err != nil {
						panic(err)
					}
					if str == "" {
						str = ss
					} else {
						str = str + "," + ss
					}
				}

			default:
				panic("undefined config type, key=" + key)
			}
		}
		err = gp.params.Save(strings.ToLower(key), str)
		if err != nil {
			panic(err)
		}

	}
```