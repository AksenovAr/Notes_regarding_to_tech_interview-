```
// you can use includes, for example:
#include <algorithm>
#include <vector>
#include <sstream>
#include <iterator>

// you can write to stdout for debugging purposes, e.g.
// cout << "this is a debug message" << endl;

int solution(string &S, string &T, string &U) {
    // write your code in C++14 (g++ 6.2.0)
    int size_of_packets = 0; 
    //conver S list of available packet server
    //  into vector
    std::stringstream ss(S);
    std::istream_iterator<std::string> begin(ss);
    std::istream_iterator<std::string> end;
    std::vector<std::string> vec(begin, end);
    std::copy(vec.begin(), vec.end(), std::ostream_iterator<std::string>(std::cout, "\n"));

    size_t pos = S.find(U);
    if (pos != std::string::npos)
    {
        // was found
        int iPacketVer =  (T.at(T.size()-1) - '0') ;

        std::cout << "iPacketVer=" << iPacketVer << std::endl;
        for ( size_t i=0; i < vec.size(); ++i)
        {
            std::vector<std::string> vec_temp;            
            std::stringstream ss_vec(vec.at(i));
            while (ss_vec.good())
            {
                std::string substr;
                getline(ss_vec, substr, ',' );
                vec_temp.push_back(substr);
            }
            std::cout << std::endl << "vec_temp.at(1)=" << vec_temp.at(1) << std::endl;
            if (std::stoi(vec_temp.at(1)) == iPacketVer)
            {
                continue;
            }
            else
            {
                // calculate size 
                size_of_packets = size_of_packets + std::stoi(vec_temp.at(2));
            }
        }
    }
    else
    {
        // not found 
        return -1;
    }
    std::cout << "size_of_packets=" << size_of_packets << std::endl;
    return size_of_packets;
}
```
