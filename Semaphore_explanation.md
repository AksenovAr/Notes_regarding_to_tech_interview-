## Semaphore main idea is start threads parallel. 
After one circle of working they stop at barierr and wait for all threads will be ready to start new raicing. 
## Semaphore has two function wait and signal.
  Wait function decrease thread counter and when it is equal zero will condition variable emit notify_all notification. Recieved this signal threads start working.
  
  Signal function increase thread counter 
  
```
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
#include <condition_variable>

using namespace std;

class MySemaphore
{
    std::mutex mut;
    std::condition_variable cv;
    int iCount;
public:
    MySemaphore(int count)
    {
        iCount = count;
    }
    
    void wait()
    {
        std::unique_lock<std::mutex> lck(mut);    
        while(iCount == 0)
        {
            cv.wait(lck );        
        }
         --iCount;
    }
    
    void signal() // 
    {
        std::unique_lock<std::mutex> lck(mut);
        iCount++;        
        cv.notify_one(); 
    }
};

MySemaphore   obj(3);
 
void job1()
{
    obj.wait();    
    std::cout << "From Job1 "  << std::endl;       
}

void job2()
{         
    obj.wait();
    std::cout << "From Job2 "  << std::endl;
}

void job3()
{   
    obj.wait();
    std::cout << "From Job3 " << std::endl;
}

int main()
{ 
    std::thread t1 (job1);
    std::thread t2 (job2);
    std::thread t3 (job3);
    
    std::cout << "Running in pararel 3 thread \n";
    
    obj.signal();
    
    t1.join();
    t2.join();
    t3.join();
    
    std::cout << "Test has finished !!!!!!";
}
```

to be continue ...
