## Semaphore main idea is start threads parallel. 
After one circle of working they stop at barierr and wait for all threads will be ready to start new raicing. 
## Semaphore has two function wait and signal.
  Wait function decrease thread counter and when it is equal zero will condition variable emit notify_all notification. Recieved this signal threads start working.
  
  Signal function increase thread counter 
  
```
std::mutex mut;
std::condition_variable cv;
std::atomic<int> iCount;

void wait()
{
    std::unique_lock<std::mutex> lck(mut);
    iCount--;
    while (iCount) cv.wait(lck);

    // Doing some job here
}

void signal() // 
{
    std::unique_lock<std::mutex> lck(mut);

    iCount++;        
    cv.notify_all();   
}
```

to be continue ...