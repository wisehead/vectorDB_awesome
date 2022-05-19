#1.IVFConfAdapter::CheckTrain

```
IVFConfAdapter::CheckTrain
--CheckIntByRange(IndexParams::nlist, MIN_NLIST, MAX_NLIST);
--CheckIntByRange(meta::ROWS, DEFAULT_MIN_ROWS, DEFAULT_MAX_ROWS);
--int64_t nq = oricfg[meta::ROWS].get<int64_t>();
  int64_t nlist = oricfg[IndexParams::nlist].get<int64_t>();
  oricfg[IndexParams::nlist] = MatchNlist(nq, nlist);
--ConfAdapter::CheckTrain
```

#2.ConfAdapter::CheckTrain

```cpp
ConfAdapter::CheckTrain(Config& oricfg, IndexMode& mode) {
    static std::vector<std::string> METRICS{Metric::L2, Metric::IP};
    CheckIntByRange(meta::DIM, DEFAULT_MIN_DIM, DEFAULT_MAX_DIM);
    CheckStrByValues(Metric::TYPE, METRICS);
    return true;
}
```