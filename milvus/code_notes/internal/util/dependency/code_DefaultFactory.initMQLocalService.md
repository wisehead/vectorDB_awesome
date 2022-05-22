#1.DefaultFactory.initMQLocalService

```
DefaultFactory.initMQLocalService
--if params.RocksmqEnable()
----msgstream.NewRmsFactory(path)
------internal.mq.msgstream.NewRmsFactory
--------f := &RmsFactory{
		dispatcherFactory: ProtoUDFactory{},
		ReceiveBufSize:    1024,
		RmqBufSize:        1024,
	}
--------err := rmqimplserver.InitRocksMQ(path)
----------inInitRocksMQ
```