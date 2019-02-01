# Notes-regarding-tech-interview-
Here I am going to make some notes regarding to tech interview questions

### What we mean when say poliorphyzm
  * There are two types of polimorphism static and dynamic. 
  It is common for polimorphism when we have one function that can do 
  different job depending on sitiation.
  For example we have fuction that should to add two big number and possible to bitness owerloading.
  
## Example program
```
#include <iostream>
#include <string>
#include <limits>
#include <exception>

using namespace std;

template <class T>
T addNumber(T& a, T& b) 
{	
	if (std::numeric_limits<T>::max() - a >= b)
	{
		return a + b;
	}
	// Here we deal with an implicit type convertion
	throw 10;
}

int main()
{
	int a = numeric_limits<int>::max() - 100;
	int b = 5000;
	try
	{
		int c = addNumber(a, b);
		std::cout << "C=" << c;
	}
	catch (...)
	{
		std::cout << "Exeption";
	}
	return (0);
}
```

### This is so called static polimorphizm. 
Compiler is creating many instances of addNumber function during compiling time.

## Runtime polimorphizm explanation
 Any function calling using virtual table is called runtime polymorphizm. Befor as give example need to explain how to virtual functions work.

If we add c++ keyword virtual befor function compiler create virtual function table and alocate ponter at it before class object in the memory.
![](https://i.imgur.com/N61b5kQ.gif)

If we have class inheritance as a below, every time befor enter to class constructor at open brace we rewrite virtual function memory shift, regarding class adress in the memory.

###Example program
```
#include <iostream>
#include <string>

using namespace std;

class A
{
    public :
    A() {
        cout << "A ctor \n";
    }
    
    ~A() {
        cout << "A dtor \n";
    }
    
    virtual void f() {
        cout << "This called from A class \n";
    }
};

class B : public A
{
    public :
    B() {
        cout << "B ctor \n";
    }
    
    ~B() {
        cout << "B dtor \n";
    }
    
    virtual void f() {
        cout << "This called from B class \n";
    }
};

int main()
{
     A* pObj = new B();
     // if void f() function is virtual will be called B variant
     // without virtual keyword called A variant
     pObj->f();   
}
```
## In the code above every time entering in the constructor at symbol { we overwrite shift of function in the virtual table.
And every time when we call any function using virtual table mechanizm it is called runtime polimorphizm.
  
  
  
  
