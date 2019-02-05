## Here we consider so called diamond inheritance when we use virtual inheritance

![](https://i.imgur.com/mBK9zvF.png)


### Example 

```
#include <iostream>
#include <string>

using namespace std;

class D
{
    public:
    D()
    {
        cout << "CTOR D \n";
    }
    ~D()
    {
        cout << "DTOR D \n";
    }
};

class B : virtual public  D
{
    public:
    B()
    {
        cout << "CTOR B \n";
    }
    ~B()
    {
        cout << "DTOR B \n";
    }
};

class C : virtual public  D
{
    public:
    C()
    {
        cout << "CTOR C \n";
    }
    ~C()
    {
        cout << "DTOR C \n";
    }
};

class A : public B, public C
{
    public:
    A()
    {
        cout << "CTOR A \n";
    }
    ~A()
    {
        cout << "DTOR A \n";
    }
};

int main()
{  
    A  obj;  
}
```
### Output 

CTOR D 
CTOR B 
CTOR C 
CTOR A 
DTOR A 
DTOR C 
DTOR B 
DTOR D 

to be continue
