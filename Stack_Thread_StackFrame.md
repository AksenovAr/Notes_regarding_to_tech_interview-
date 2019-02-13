## Every thread has his own stack assotiated with its.

Stack frame is a part of stack assosiated with function
that called in thread.

Frame contents function arguments, function return adress (from function where called), local values. 

## ESP is the current stack pointer. EBP is the base pointer for the current stack frame

## Where is the code of fuction stored

![](https://i.imgur.com/FtOGCvy.jpg)

### In c++ 11 and higher we can use values  in many threads and behaviour will not be undefined

''' Global
           atomic<int> x, y;

Thread 1                 Thread 2
x.store(17);             cout << y.load() << " ";
y.store(37);             cout << x.load() << endl;'''
