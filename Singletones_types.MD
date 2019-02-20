## Scott Meyers singletone vs ordinary singletone

### Here the code of Scott Mayes singletone and it is preferable than ordinary by follow reasons :
#### Advantages    
    * It is thread safe, becouse memory for static objects allocated by compiler at compiling process
    * Easy for understanding
#### Limitations
    * It correct works since C++11 version
    
### Example program
```
#include <iostream>
#include <string>

using namespace std;

class MySingletone
{
    public :
    
    static MySingletone& Instance()
    {
        static MySingletone obj;
        return obj;
    }
    
    static void isWork()
    {
        std::cout <<  " It is working \n ";
    }
    
    MySingletone() { cout << " Ctor singltone ! \n" ;} ;
    ~MySingletone() { cout << " Dtor singltone ! \n" ;} ;
     
    private:
     
    MySingletone&  operator = (const MySingletone& )  = delete;
    MySingletone&  operator = (const MySingletone&& ) = delete;
    MySingletone( const MySingletone& ) = delete;
    MySingletone( const MySingletone&& ) = delete;
};

int main()
{
    MySingletone& obj = MySingletone::Instance();
    obj.isWork();
}
```

### Below I placed ordinary singletone code example  :
#### It is match more complicated need use sincronization objects to
make it safe. As we can see we should care aboure object deleting and provide multhithreading correct work.
      
#### Example program
```
#include <iostream>
#include <string>

using namespace std;

class mySingleton
{
public:
	static mySingleton * Instance()
	{
		if(!self_)
		{
			self_ = new mySingleton();
			return self_;
		}
		return nullptr;
	}

	static bool kill()
	{
		if(self_)
		{
			delete self_;
			return true;
		}
		return false;
	}
	static void isWork()
	{
	    cout << "I am working \n ";
	}
private:
	mySingleton() {};
	~mySingleton() {};
	mySingleton(const mySingleton& copy) {};
	mySingleton& operator = (const mySingleton& copy) {};
private:
	static mySingleton *self_;

};
mySingleton *mySingleton::self_ = 0;

int main()
{
    mySingleton* pObj = mySingleton::Instance();
    pObj->isWork();
    pObj->kill();
}
```
### Below we consider the best variant of singletone IMHO

```
class MySingletone
{
    public :
    
    static shared_ptr<MySingletone> getInstance()
    {
        std::cout <<  " Enter in getInstance \n ";
        static shared_ptr<MySingletone> obj(new MySingletone);
        return obj;
    }
        
    void isWork()
    {
        std::cout <<  " It is working \n ";
    }
   
     MySingletone() { cout << " Ctor singltone ! \n" ;} ;
    ~MySingletone() { cout << " Dtor singltone ! \n" ;} ;
    
    private:
           
    MySingletone&  operator = (const MySingletone& )  = delete;
    MySingletone&  operator = (const MySingletone&& ) = delete;
    MySingletone( const MySingletone& ) = delete;
    MySingletone( const MySingletone&& ) = delete;
};

int main()
{
    shared_ptr<MySingletone> obj( MySingletone::getInstance() );
    obj->isWork();
}
```

## Conclusion
   Based on static type singletone match more preferable than based on memory aloocated in the heap. Inthe second case we should worried about safethread becouse if in the row number 68 task context switch will occur memory will be alocate two times.
