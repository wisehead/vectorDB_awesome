#1.DefaultFactory::initMQRemoteService

```go
DefaultFactory::initMQRemoteService
--if params.PulsarEnable() {
----return msgstream.NewPmsFactory(&params.PulsarCfg)
	}

--if params.KafkaEnable() {
----return msgstream.NewKmsFactory(&params.KafkaCfg)
	}
```