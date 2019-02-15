## There are three smart ptr variants in modern C++
that cover needs.

1. unique_ptr
2. std::shared_ptr
3. std::weak_ptr

### Example of unique_ptr
 
 Place here example
 
 ### Code example of shared_ptr

deleted for  improvment

## Here people make notice to that implementation
https://codereview.stackexchange.com/questions/140693/shared-ptr-code-implementation

### If we use c++ exeption in object constructor we can not use smart pointers gived above.

For this cases we should use the follow analog of smart pointers 
1. make_unique
2. make_shared
3. make_weak

The reason why we should do it the follow destructor is not called for undone constructor and for unique_prt object will not be destroyed. For shared and weak ptr object handle counter lost count. 

### Importante notice !

auto_ptr smart pointer depricated since c++ 11 appeared.
There are two reason  why:
1. modern variant auto_ptr has been using 

```
std::unique_ptr<int> p2 = std::move(p);
```

2. auto ptr can not call delete [] for array of values

### Never throw c++ exeption in the object desructor 
It leads to undefined behaviour and may raise terminate OS signal. Stack reversing back in exeption case and we call destructor for another objects. If other objects raise exception too start once reversing stack process and two process can meet with terminate signal.



