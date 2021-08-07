'''
// you can use includes, for example:
#include <algorithm>

// you can write to stdout for debugging purposes, e.g.
// cout << "this is a debug message" << endl;

int solution(vector<int> &A) {
    // write your code in C++14 (g++ 6.2.0)
    std::sort(A.begin(), A.end());
    int ret =0;
    for (size_t x=0; x < A.size()-1; ++x)
    {
        int iCur = A.at(x);
        int iNext = A.at(x+1);
        if (iNext - iCur > 1)
        {
            ret = iCur+1;
        }
    }
    if (ret == 0 && A.size()) ret = ++A.at( A.size()-1 );
    if (ret < 0) ret = 1;
    return ret;
}
'''
