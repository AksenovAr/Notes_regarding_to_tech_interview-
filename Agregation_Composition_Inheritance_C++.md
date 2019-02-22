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
### Composition
#### Example of code 
```
class A
{
private:
 
public:
    A() { cout << "Of A +" << endl; }
    ~A(){ cout << "Of A -" << endl; }
    
};
 
class B 
{
private:
    A classInClass;
public:
    B() { cout << "Of B +" << endl; }
    ~B(){ cout << "Of B -" << endl; }
    
};
 
int main()
{
    B ptr;
    return 0;
}
```
### Agregation 
#### Example of code 

```
class A
{
private:
 
public:
    A() { cout << "Of A +" << endl; }
    ~A(){ cout << "Of A -" << endl; }
    
};
 
class B 
{
private:
    A* classInClass;
public:
    B()
    {
        classInClass = new A();
        cout << "Of B +" << endl; 
    }
    ~B()
    {
        delete classInClass;        
        cout << "Of B -" << endl; 
    }
    
};
 
int main()
{
    B ptr;
    return 0;
}
```
