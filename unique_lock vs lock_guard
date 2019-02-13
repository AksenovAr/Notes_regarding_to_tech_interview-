
## The difference is that you can lock and unlock a std::unique_lock .
std::lock_guard will be locked only once on construction and unlocked on destruction. 
... std::unique_lock has other features that allow it to e.g.:
be constructed without locking the mutex immediately but to build the RAII wrapper (see here)
