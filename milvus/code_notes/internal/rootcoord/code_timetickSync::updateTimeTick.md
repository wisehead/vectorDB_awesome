#1.timetickSync::updateTimeTick

```
updateTimeTick
--prev, ok := t.sess2ChanTsMap[in.Base.SourceID]
--// if ddl operation not finished, skip current ts update
--ddlMinTs := t.getDdlMinTimeTick()
---- t.ddlMinTs
```