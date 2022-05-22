#1.timetickSync::updateTimeTick

```
updateTimeTick
--prev, ok := t.sess2ChanTsMap[in.Base.SourceID]
--// if ddl operation not finished, skip current ts update
--ddlMinTs := t.getDdlMinTimeTick()
---- t.ddlMinTs
--if prev == nil {
----t.sess2ChanTsMap[in.Base.SourceID] = newChanTsMsg(in, 1)
--} else {
----t.sess2ChanTsMap[in.Base.SourceID] = newChanTsMsg(in, prev.cnt+1)
--t.sendToChannel()
```