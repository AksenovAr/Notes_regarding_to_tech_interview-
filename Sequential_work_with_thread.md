## We should provide to job2 tread start after job1 finishing
From intially programm looks like below. This version is not satisfied to conditions.

### Example program
```
#include <iostream>
#include <string>
#include <thread>

void job1() {
    for( int i=0; i < 10; ++i)
        std::cout << "Hello, from job1" << std::endl;    
}

void job2() {
    for( int i=0; i < 10; ++i)
        std::cout << "Hello, from job2" << std::endl;    
}

int main()
{
   std::thread t1(job1);
   std::thread t2(job2);      
   t1.join();
   t2.join();
}
```
### Code below is works as demanded

To reach it we need one mutex one condition variable and one bool value. 

###Example program
```
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
#include <condition_variable>

std::mutex g_mutex;
std::condition_variable cv;
bool ready = false;

void job1()
{
     std::unique_lock<std::mutex> lg(g_mutex);
    
    for( int i=0; i < 10; ++i)
        std::cout << "Hello, from job1" << std::endl;    
    
    ready = true;
    cv.notify_all();
}

void job2()
{
    std::unique_lock<std::mutex> lg(g_mutex);
    
    cv.wait( lg, [] () { return ready; });
    for( int i=0; i < 10; ++i)
        std::cout << "Hello, from job2" << std::endl;    
}

int main()
{
   std::thread t1(job1);
   std::thread t2(job2);      
   t1.join();
   t2.join();
}
```
