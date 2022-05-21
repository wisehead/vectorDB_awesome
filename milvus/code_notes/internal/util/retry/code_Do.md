#1.Do

```go
	for i := uint(0); i < c.attempts; i++ {
		if err := fn(); err != nil {
			if i%10 == 0 {
				log.Debug("retry func failed", zap.Uint("retry time", i), zap.Error(err))
			}

			el = append(el, err)

			if ok := IsUnRecoverable(err); ok {
				return el
			}

			select {
			case <-time.After(c.sleep):
			case <-ctx.Done():
				el = append(el, ctx.Err())
				return el
			}

			c.sleep *= 2
			if c.sleep > c.maxSleepTime {
				c.sleep = c.maxSleepTime
			}
		} else {
			return nil
		}
	}
	return el
```