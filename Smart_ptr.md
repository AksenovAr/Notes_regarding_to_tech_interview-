## There are three smart ptr variants in modern C++
that cover needs.

1. unique_ptr
2. std::shared_ptr
3. std::weak_ptr

### Example of unique_ptr
 
 Place here example
 
 ### Code example of shared_ptr
 
```
template<typename T>
class MySharedPtr
{    
    MySharedPtr( const T* pObj ): m_pObj(nullptr), mp_count(nullptr)
    {
        m_pObj = pObj;
        mp_count = new int(1);
    }
    
    MySharedPtr( const MySharedPtr & obj )
    {
        m_pObj = obj.m_pObj;
        Increment();                  
    }
    
    ~MySharedPtr( const MySharedPtr & obj)    
    {   
        Decrement();
        if( m_pObj && m_count == 0)
        {
            delete m_pObj;
            m_pObj = nullptr;
            delete mp_count;
            mp_count = nullptr;
        }
    }

    MySharedPtr& operator = ( const MySharedPtr & obj )
    {
        if ( this !=  &obj)
        {
            m_pObj = obj.m_pObj;
            Increment();                   
        }        
        return this;
    }
    
    T* operator -> () const 
    {
        return m_pObj;
    }
    
    
    T& operator*() const 
    {
        return *pt; 
    }
    
    
    private:
    void Increment()
    {
        (*mp_count)++;
        
    }
    void Decrement()
    {
        (*mp_count)--;
    }
    
    //deep copy -- need to change it in all instance
    int* mp_count;
    T* m_pObj;
};
```

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



