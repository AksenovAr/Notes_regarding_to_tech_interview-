# Notes-regarding-tech-interview-
Here I am going to make some notes regarding to tech interview questions
Let`s consider the follow example. If we look at output we may see that 
destructor for D class was not called. It can lead to memory leak. To avoid 
such horrible situation we should use virtual desructor.

### Example program
#include <iostream>
#include <string>

using namespace std;

class A
{
public:
    A() {
        cout << "A ctor \n"; }
    
    ~A() {
        cout << "A dtor \n"; }    
};

class B : public A
{
public:
    B() {
        cout << "B ctor \n"; }
    
    ~B() {
        cout << "B dtor \n"; }        
};

int main()
{
  A* pAobject = new B();
  delete pAobject;
}
### Output is :
A ctor 
B ctor 
A dtor 
B class destructor there is no called.

### How to call B class destructor and avoid potential danger situation
* We should use virtual function properties 
* I will discribe how it works it the separate note 
* Lets make A class destructor is virtual and o Magic 
 
 virtual ~A() {
        cout << "A dtor \n"; }    
* Enough to to add magic word virtual and we can see another picture
### Output is :

A ctor 
B ctor 
B dtor 
A dtor 

### All start working as expected
