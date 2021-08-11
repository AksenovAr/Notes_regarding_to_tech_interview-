```
#include <iostream>
#include <string>
#include <vector>

int findClosestNumber( std::vector<int>& arr, int x)
{
    int best = arr[0];
    for ( size_t i=0; i < arr.size(); ++i )
    {
        best = std::abs( arr[i]-x) < std::abs(best -x) ? arr[i] : best;
    }
    return best;
}


int solution ( int x, int y )
{
    std::vector <int> vec = { -135, -90, -30, 0, 30, 90, 135, 180 };
    int angle = 180-(x-y);
    angle = angle%360;
    int closest = findClosestNumber(vec, angle );
    return closest;
}

int main()
{
  
  int x= 5;
  int y = 200; 
  std::cout << "angle, " << solution(x, y) << "!\n";
  
  x= 270;
  y = 50; 
  std::cout << "angle, " << solution(x, y) << "!\n";
}
```
