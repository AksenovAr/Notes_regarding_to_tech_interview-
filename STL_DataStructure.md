### Here I want to share with other developer with my thoughts regarding to STL data Structure.

### Red-Black tree based containers.

1. Set and Multiset
2. Map and Multimap

Red-black tree it is a selfbalanced binary tree.
It has finding O (log N)
If we remove or delete some node from tree it may need to reorganize, for example to do it tree should rotate and it can take match more time then logN.

### Vector based on random access iterator

1. Vector should be allocated in memory as hole part. Find operation does not depend on N. If we remove or add some elements we have to move hole pat of memory and it is not depent on elements count.

### List container based on sequential iterator

To find some element we shoud pass all elements in containers in the worst case.

Delete and Remove operation do not require moving other elements in the memory.

### Stack and Queue have no iterator and introduce yourself adapter. 
