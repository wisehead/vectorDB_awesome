#1.HNSWConfAdapter::CheckTrain

```
HNSWConfAdapter::CheckTrain
--CheckIntByRange(meta::ROWS, DEFAULT_MIN_ROWS, DEFAULT_MAX_ROWS);
--CheckIntByRange(IndexParams::efConstruction, MIN_EFCONSTRUCTION, MAX_EFCONSTRUCTION);
--CheckIntByRange(IndexParams::M, MIN_M, MAX_M);
--ConfAdapter::CheckTrain(oricfg, mode);
```

#2.ConfAdapter::CheckTrain

```cpp
	 static std::vector<std::string> METRICS{Metric::L2, Metric::IP};
    CheckIntByRange(meta::DIM, DEFAULT_MIN_DIM, DEFAULT_MAX_DIM);
    CheckStrByValues(Metric::TYPE, METRICS);
```