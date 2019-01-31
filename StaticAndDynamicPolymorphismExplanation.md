# Notes-regarding-tech-interview-
Here I am going to make some notes regarding to tech interview questions

### What we mean when say poliorphyzm
  * There are two types of polimorphism static and dynamic. 
  It is common for polimorphism when we have one function that can do 
  different job depending on sitiation.
  For example we have fuction that should to add two big number and possible to bitness awerloading.
  
## Example program
#include <iostream>
#include <string>
#include <limits>
#include <exception>

using namespace std;

template <class T>
T addNumber(T& a, T& b) 
{	
	if (std::numeric_limits<T>::max() - a >= b)
	{
		return a + b;
	}
	// Here we deal with an implicit type convertion
	throw 10;
}

int main()
{
	int a = numeric_limits<int>::max() - 100;
	int b = 5000;
	try
	{
		int c = addNumber(a, b);
		std::cout << "C=" << c;
	}
	catch (...)
	{
		std::cout << "Exeption";
	}
	return (0);
}

### This is so called static polimorphizm. 
Compiler is creating many instances of addNumber function during compiling time.

To be continue ... 
  
  
  
  
