```
#include <iostream>
#include <string>


class integer
{
    public:
    int x;    
    integer(int r)
    {
        x = r;
    }
    
    integer& operator ++()
    {
        ++this->x;
        return *this;
    }
    
    integer operator ++(int r)
    {
        integer a(r);
        ++this->x;
        return a;
    }
    
};
        

int main()
{
  integer ob(2);
  ++ob;
  ob++;
  std::cout << "Hello, " << ob.x << "!\n";
}
    ```
