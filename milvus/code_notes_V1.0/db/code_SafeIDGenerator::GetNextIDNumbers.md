#1.SafeIDGenerator::GetNextIDNumbers

```
SafeIDGenerator::GetNextIDNumbers
--while (n > 0) {
----if (n > MAX_IDS_PER_MICRO) {
------Status status = NextIDNumbers(MAX_IDS_PER_MICRO, ids);
--------SafeIDGenerator::NextIDNumbers
------n -= MAX_IDS_PER_MICRO;
----else {
------Status status = NextIDNumbers(n, ids);
------break;
```

#2.SafeIDGenerator::NextIDNumbers

```
SafeIDGenerator::NextIDNumbers
--auto now = std::chrono::system_clock::now();
--int64_t micros = std::chrono::duration_cast<std::chrono::microseconds>(now.time_since_epoch()).count();
--if (micros <= time_stamp_ms_) {
----time_stamp_ms_ += 1;
--} else {
----time_stamp_ms_ = micros;
--int64_t ID_high_part = time_stamp_ms_ * MAX_IDS_PER_MICRO;
--for (size_t pos = 0; pos < n; ++pos) {
        ids.push_back(ID_high_part + pos);
--}

```