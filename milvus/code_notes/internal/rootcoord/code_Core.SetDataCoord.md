#1.Core.SetDataCoord

```
SetDataCoord
--initCh := make(chan struct{})
--go func() 
----s.Init()
------internal.distributed.datanode.client.Client.Init
----s.Start();
--c.CallGetBinlogFilePathsService
--c.CallGetNumRowsService
--c.CallGetFlushedSegmentsService
--c.CallWatchChannels
--c.CallImportService
--c.CallFlushOnCollection
```

#2.c.CallGetBinlogFilePathsService

```go
c.CallGetBinlogFilePathsService = func(ctx context.Context, segID typeutil.UniqueID, fieldID typeutil.UniqueID) (retFiles []string, retErr error) {
		defer func() {
			if err := recover(); err != nil {
				retErr = fmt.Errorf("get bin log file paths panic, msg = %v", err)
			}
		}()
		<-initCh //wait connect to DataCoord
		ts, err := c.TSOAllocator(1)
		if err != nil {
			return nil, err
		}
		binlog, err := s.GetInsertBinlogPaths(ctx, &datapb.GetInsertBinlogPathsRequest{
			Base: &commonpb.MsgBase{
				MsgType:   0, //TODO, msg type
				MsgID:     0,
				Timestamp: ts,
				SourceID:  c.session.ServerID,
			},
			SegmentID: segID,
		})
		if err != nil {
			return nil, err
		}
		if binlog.Status.ErrorCode != commonpb.ErrorCode_Success {
			return nil, fmt.Errorf("getInsertBinlogPaths from data service failed, error = %s", binlog.Status.Reason)
		}
		binlogPaths := make([]string, 0)
		for i := range binlog.FieldIDs {
			if binlog.FieldIDs[i] == fieldID {
				binlogPaths = append(binlogPaths, binlog.Paths[i].Values...)
			}
		}
		if len(binlogPaths) == 0 {
			return nil, fmt.Errorf("binlog file does not exist, segment id = %d, field id = %d", segID, fieldID)
		}
		return binlogPaths, nil
	}
```

#3. c.CallGetNumRowsService

```go
c.CallGetNumRowsService = func(ctx context.Context, segID typeutil.UniqueID, isFromFlushedChan bool) (retRows int64, retErr error) {
		defer func() {
			if err := recover(); err != nil {
				retErr = fmt.Errorf("get num rows panic, msg = %v", err)
			}
		}()
		<-initCh
		ts, err := c.TSOAllocator(1)
		if err != nil {
			return retRows, err
		}
		segInfo, err := s.GetSegmentInfo(ctx, &datapb.GetSegmentInfoRequest{
			Base: &commonpb.MsgBase{
				MsgType:   0, //TODO, msg type
				MsgID:     0,
				Timestamp: ts,
				SourceID:  c.session.ServerID,
			},
			SegmentIDs: []typeutil.UniqueID{segID},
		})
		if err != nil {
			return retRows, err
		}
		if segInfo.Status.ErrorCode != commonpb.ErrorCode_Success {
			return retRows, fmt.Errorf("getSegmentInfo from data service failed, error = %s", segInfo.Status.Reason)
		}
		if len(segInfo.Infos) != 1 {
			log.Debug("get segment info empty")
			return retRows, nil
		}
		if !isFromFlushedChan && segInfo.Infos[0].State != commonpb.SegmentState_Flushed {
			log.Debug("segment id not flushed", zap.Int64("segment id", segID))
			return retRows, nil
		}
		return segInfo.Infos[0].NumOfRows, nil
	}
```

#4. c.CallGetFlushedSegmentsService

```go
c.CallGetFlushedSegmentsService = func(ctx context.Context, collID, partID typeutil.UniqueID) (retSegIDs []typeutil.UniqueID, retErr error) {
		defer func() {
			if err := recover(); err != nil {
				retErr = fmt.Errorf("get flushed segments from data coord panic, msg = %v", err)
			}
		}()
		<-initCh
		req := &datapb.GetFlushedSegmentsRequest{
			Base: &commonpb.MsgBase{
				MsgType:   0, //TODO,msg type
				MsgID:     0,
				Timestamp: 0,
				SourceID:  c.session.ServerID,
			},
			CollectionID: collID,
			PartitionID:  partID,
		}
		rsp, err := s.GetFlushedSegments(ctx, req)
		if err != nil {
			return nil, err
		}
		if rsp.Status.ErrorCode != commonpb.ErrorCode_Success {
			return nil, fmt.Errorf("get flushed segments from data coord failed, reason = %s", rsp.Status.Reason)
		}
		return rsp.Segments, nil
	}

```

#5. c.CallWatchChannels

```go
	c.CallWatchChannels = func(ctx context.Context, collectionID int64, channelNames []string) (retErr error) {
		defer func() {
			if err := recover(); err != nil {
				retErr = fmt.Errorf("watch channels panic, msg = %v", err)
			}
		}()
		<-initCh
		req := &datapb.WatchChannelsRequest{
			CollectionID: collectionID,
			ChannelNames: channelNames,
		}
		rsp, err := s.WatchChannels(ctx, req)
		if err != nil {
			return err
		}
		if rsp.Status.ErrorCode != commonpb.ErrorCode_Success {
			return fmt.Errorf("data coord watch channels failed, reason = %s", rsp.Status.Reason)
		}
		return nil
	}

```

#6 c.CallImportService
```go

	c.CallImportService = func(ctx context.Context, req *datapb.ImportTaskRequest) *datapb.ImportTaskResponse {
		resp := &datapb.ImportTaskResponse{
			Status: &commonpb.Status{
				ErrorCode: commonpb.ErrorCode_Success,
			},
		}
		defer func() {
			if err := recover(); err != nil {
				resp.Status.ErrorCode = commonpb.ErrorCode_UnexpectedError
				resp.Status.Reason = "assign import task to data coord panic"
			}
		}()
		resp, _ = s.Import(ctx, req)
		return resp
	}


```

#7. c.CallFlushOnCollection

```go
	c.CallFlushOnCollection = func(ctx context.Context, cID int64, segIDs []int64) error {
		resp, err := s.Flush(ctx, &datapb.FlushRequest{
			Base: &commonpb.MsgBase{
				MsgType:  commonpb.MsgType_Flush,
				SourceID: c.session.ServerID,
			},
			DbID:         0,
			SegmentIDs:   segIDs,
			CollectionID: cID,
		})
		if err != nil {
			return errors.New("failed to call flush to data coordinator: " + err.Error())
		}
		if resp.Status.ErrorCode != commonpb.ErrorCode_Success {
			return errors.New(resp.Status.Reason)
		}
		log.Info("flush on collection succeed", zap.Int64("collection ID", cID))
		return nil
	}
```