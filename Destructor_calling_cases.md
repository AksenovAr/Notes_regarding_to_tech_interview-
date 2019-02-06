## There are three cases when class destructor can be called
1. When object leave visibility scope.
2. When we called destructor with delete operator.
3. When compiler handle exeption in try and stack reversing towads to catch.

## Importante notice !
For the unsuccessful created constructor destructor will not be called.

## Threre are two type of new operator

1. First variant - ordinary new when OS allocate memody and then compiler place the object at this place.
2. Second - so called replacement new when compiler try to place the object at already exist place without memory allocation.
### Syntax:
new (address) (type) initializer
### Example
```
// buffer on stack 
unsigned char buf[sizeof(int)*2] ; 
  
// placement new in buf 
int *pInt = new (buf) int(3); 
```
to be continue
