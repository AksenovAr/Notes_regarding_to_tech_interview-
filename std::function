## std::function

### std::function is a templated object that is used to store and call any callable type, such as functions, objects, lambdas and the result of std::bind.

### Simple example
```
#include <iostream>
#include <functional>
using namespace std;

void global_f() {
	cout << "global_f()" << endl;
}

struct Functor {
	void operator()() { cout << "Functor" << endl; }
};

int main() {
	std::function<void()> f;
	cout << "sizeof(f) == " << sizeof(f) << endl;

	f = global_f;
	f();

	f = [](){ cout << "Lambda" << endl;};
	f();

	Functor functor;
	f = functor;
	f();
}
```
### Output:

```
sizeof(f) == 32
global_f()
Lambda
Functor
```

### How do i write a pointer-to-member-function with std::function?

```
struct Type
{
public:
    int Foo();
};
The correct syntax to store this member function in a std::function is:

std::function<int(Type&)> fooCaller = &Type::Foo;
```

### If you want to preserve the argument list (in your case, int(double)), then you need to provide the instance outside of the function. This can be done via std::bind:

```
struct A{ 
int fn(double){ return 0; } 
};

A anInstance;
std::function<int(double)> fnCaller = std::bind(&A::fn, &anInstance, std::placeholders::_1);
```

