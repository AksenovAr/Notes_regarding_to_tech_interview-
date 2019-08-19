## There are three smart ptr variants in modern C++
that cover needs.

1. unique_ptr
2. std::shared_ptr
3. std::weak_ptr

### Example of unique_ptr
 
 ```
template<typename T>
class myUnique_ptr
{
    myUnique_ptr(const T* pObj)
    : m_pData(pObj)
    {
    }
    
    ~myUnique_ptr()
    {
        if (m_pData)
        {
            delete m_pData;
        }
    }
    
    // Copy constructor
    myUnique_ptr(const myUnique_ptr& obj)
    {
        m_pData = std::move( obj.m_pData );
        obj.m_pData = nullptr;
    }
    
    // Move constructor
    myUnique_ptr(myUnique_ptr&& obj)
    {
        m_pData = std::move( obj.m_pData );
        obj.m_pData = nullptr;
    }
    
    // assigment operator
    myUnique_ptr& operator =  (const myUnique_ptr& obj)
    {
        if (this == &obj) return *this;
        
        m_pData = std::move( obj.m_pData );
        obj.m_pData = nullptr;
        
        return *this;
    }
    
     // assigment operator
    myUnique_ptr& operator =  (myUnique_ptr&& obj)
    {
        if (this == &obj) return *this;
        
        m_pData = std::move( obj.m_pData );
        obj.m_pData = nullptr;
        
        return *this;
    }
    
    T* m_pData;  
};
 ```
 
 ### Code example of shared_ptr
 
```
template<class T>
class MySharedPtr
{
    public:
    
    //Constructor
    MySharedPtr(const T* pObj)
    :m_pCountOfReference(nullptr),  m_pData(nullptr)
    {
        m_pData = pObj;
        m_pCountOfReference = new int(1);
    }
    
    //Destructor
    ~MySharedPtr()
    {
         (*m_pCountOfReference)--;
         if( (*m_pCountOfReference) == 0 )
         {
            delete m_pData;
         }
    }
    
    //Copy constructor
    MySharedPtr(const MySharedPtr& pObj)
    {
         m_pCountOfReference = pObj.m_pCountOfReference;
        (*m_pCountOfReference)++;
        m_pData = pObj.m_pData;
    }
    
    //Move constructor
    MySharedPtr(const MySharedPtr&& pObj)
    {
         m_pCountOfReference = pObj.m_pCountOfReference;
        (*m_pCountOfReference)++;
        m_pData = pObj.m_pData;
    }
    
    //operator = 
     MySharedPtr<T>& operator = (const  MySharedPtr<T>& pObj)
    {
        if( this == &pObj ) return *this;
        
        if ( *m_pCountOfReference == 1 )
        {
            delete m_pCountOfReference;
            delete m_pData;
        }
        
        m_pCountOfReference = pObj.m_pCountOfReference;
        (*m_pCountOfReference)++;
        m_pData = pObj.m_pData;
        
        return *this;
    }
    
    //move operator = 
    MySharedPtr<T>& operator = (const  MySharedPtr<T>&& pObj)
    {
        if( this == &pObj )  return *this;
        
        if ( *m_pCountOfReference == 1 )
        {
            delete m_pCountOfReference;
            delete m_pData;
        }
        
        m_pCountOfReference = pObj.m_pCountOfReference;
        (*m_pCountOfReference)++;
        m_pData = pObj.m_pData;
        
        return *this;
    }
    
    T* operator->() const
    {                
        return m_pData;
    }
    
    private:
    int * m_pCountOfReference;
    T * m_pData;
};
```

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



