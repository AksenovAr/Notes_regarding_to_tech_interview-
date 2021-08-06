```
#include <iostream>
#include <string>
#include <bitset>
//посчитать количество nill
int main()
{
   int var = 250; // 11111010
    var =~var;
   int max = 0;
   int count_of_zero = 0;
   std::bitset<32> b1(var);
   for ( size_t i=0; i < 31; ++i)
   {
       std::cout << b1.test(i) << std::endl;
       if ( b1.test(i) ) 
       {
           
           if ( b1.test(i+1) )
           {
                count_of_zero++;           
           }
           else
           {
                max = std::max( max, count_of_zero);
                count_of_zero =0;
           }
       }
       max = std::max( max, count_of_zero);
       
       //
   }  
   std:: cout << max+1;
}
```
