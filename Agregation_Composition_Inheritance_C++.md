## Composition, agregation and inheritance in C++

### Inheritance 
#### Example of code 
```
class A
{
public:
    A() { cout << "Of A +" << endl; }
    ~A(){ cout << "Of A -" << endl; }
    void f() { cout << "I am from A" << endl; }
};
 
class B : public A
{
public:
    B() { cout << "Of B +" << endl; }
    ~B(){ cout << "Of B -" << endl; }
    void f() { cout << "I am from B" << endl; }
};
 
int main()
{
    A* ptr = new B();
    ptr->f();
    delete ptr;
 
    return 0;
}
```

...To be cotinued

Remeved for improvements
