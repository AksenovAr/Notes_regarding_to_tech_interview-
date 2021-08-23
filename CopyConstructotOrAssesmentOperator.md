
```
#include <iostream>
#include <string>

struct Foo
{
    public:
    int x;
    Foo(int e) : x(e)
    {
    }
    Foo(const Foo& a)
    {
        x=a.x;
        x++;
    }
    Foo& operator=( const Foo& a1 )
    {
        x=a1.x;
        x--;
        return *this;
    }
};

int main()
{
 
   Foo a(4);
   Foo b = a;
   std::cout << b.x;
}
  
  output 5 (copy ctor)
  
```
