### Here I would like to consider follow function

#include <iostream>
#include <cstring>

using namespace std;

```
int cancatenate_two_str( const char* p_str1, const char* p_str2, char*& p_result_string )
{
    int ret = strlen(p_str1) + strlen(p_str2);
    if (p_result_string == nullptr)
    {
        p_result_string = new char[ret];
    }
    else
    {
        delete p_result_string;
        p_result_string = new char[ret];
    }
    
    p_result_string = strcat(p_result_string, p_str1);
    p_result_string = strcat(p_result_string, p_str2);
    
}

int main()
{
    char str1[] = "Mari +";
    char str2[] = " Andrey = Love";
    char*p_res_str = nullptr;
    
    cancatenate_two_str(str1, str2, p_res_str);
    
    cout<< std::string(p_res_str);

    return 0;
}
```

### Noticed, if we pass in function pointer at string array we should pass pointer by reference or ponter at pointer.
