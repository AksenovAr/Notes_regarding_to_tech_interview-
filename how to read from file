### Несколько способов чтения из файла на с++
#### Для любого способа надо открыть файл и закрыть после использования, так же необходима проверка на то что файл открылся. 
```
#include <iostream>
#include <fstream>

using namespace std;

int main()
{
    std::ifstream input( "filename.ext" );
    if (!input.is_open()) return -1;
    
    
    input.close();
    return 0;
}

```

#### Чтение построчно 
```
for( std::string line; getline( input, line ); )
{
    ...for each line in input...
}
```
#### Чтение отдельных символов
```
int x, y;
input >> x >> y;
```

#### Чтение из файла посимвольно 
```
char my_character ;
int number_of_lines = 0;
while (!input.eof() )
{
    input.get(my_character);        
	if (my_character == '\n')
	{
	    ++number_of_lines;
	}
}
```
#### Парсинг строки (Mystring входная строка прим. 2 4 5 6 )
```
 std::stringstream iss( myString );

 int number;
 std::vector<int> myNumbers;
 while ( iss >> number )
  myNumbers.push_back( number );

```
