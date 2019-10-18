#### Немного о списках инициализации

```
// Example program
#include <iostream>
#include <string>

class party 
{
    public:
    party( int i_boys) : boys(i_boys), girls(boys*2)
    {
    }
    
    int girls;
    int boys;
    
    void print_f()
    {
        std::cout << "boys are " << boys << " girls are " << girls;
    }
};

int main()
{
  party ob(5);
  ob.print_f();
}

Вывод: boys are 5 girls are 0 
```
####    Дело в том что компиляторы С++ инициализируют список инициализации строго в том порядке как обявлены переменные в заголовочном файле. ТО есть в данном слечае сначало девочки будут инициализированы а по том мальчики. А так как количесство мальчиком не изместно то тут возможно два варианта или мусором из памяти будет переменная инициализирована или нулем.
