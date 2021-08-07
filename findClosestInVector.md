// Example program
#include <iostream>
#include <string>
#include <vector>

int findClosestNumber( std::vector<int>& arr, int x)
{
    int best = arr[0];
    for ( int i=0; i < arr.size(); ++i )
    {
        best = std::abs( arr[i]-x) < std::abs(best -x) ? arr[i] : best;
    }
    return best;
}

int main()
{
   std::vector<int> vec = {-10,0,5, 34, 234};
   int iFind = 35;
   std::cout << "closest to  = "  << iFind << " is :" << findClosestNumber( vec, iFind) << std::endl;
}
