### Пример записи в файл на с++
```
#include <fstream>
#include <string>
#include <iostream>

int main()
{
    std::string input("Something to file");
    std::ofstream out("output.txt");
    if (!out.is_open() ) return -1;
    out << input;
    out.close();
    return 0;
}

```
