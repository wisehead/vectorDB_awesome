#1.InstanceLockCheck::Check

```cpp
InstanceLockCheck::Check
--fd = open(lock_path.c_str(), O_RDWR | O_CREAT | O_NOFOLLOW, 0640);
-- // Acquire a write lock
    struct flock fl;
    // exclusive lock
    fl.l_type = F_WRLCK;
    fl.l_whence = SEEK_SET;
    fl.l_start = 0;
    fl.l_len = 0;
    auto fcl = fcntl(fd, F_SETLK, &fl);

```