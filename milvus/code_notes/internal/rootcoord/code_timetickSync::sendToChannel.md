#1.timetickSync::sendToChannel

```
timetickSync::sendToChannel
--idleSessionList := make([]typeutil.UniqueID, 0, len(t.sess2ChanTsMap))
--// clear sess2ChanTsMap and send a clone
	ptt := make(map[typeutil.UniqueID]*chanTsMsg)
	for k, v := range t.sess2ChanTsMap {
		ptt[k] = v
		t.sess2ChanTsMap[k] = nil
	}
	t.sendChan <- ptt
```