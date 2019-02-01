## Let`s consider the follow example

### Example program

```
#include <iostream>
#include <string>

using namespace std;

class A
{
public:
A() {
cout << "A ctor \n";
}
~A(){
cout << "A dtor \n";
}

};

class B
{
public:
B() {
cout << "B ctor \n";
}
~B() {
cout << "B dtor \n";
}

};

class o1
{
public:
o1() {
cout << "o1 ctor \n";
}
~o1() {
cout << "o1 dtor \n";
}
};

class o2
{
public:
o2() {
cout << "o2 ctor \n";
}
~o2() {
cout << "o2 dtor \n";
}
};

class C : public B, public A
{
public:
C() {
cout << "C ctor \n";
}
~C() {
cout << "C dtor \n";
}
o1 obj1;
o2 obj2;    
};


int main()
{
C obj;  
}
```
The output of this code will be 

B ctor
A ctor 
o1 ctor 
o2 ctor 
C ctor 
//Since place objects start destoring in reverse order
C dtor 
o2 dtor 
o1 dtor 
A dtor 
B dtor 

###As we can see compiler create from left to right and up to down and destoy it in reverse order.


