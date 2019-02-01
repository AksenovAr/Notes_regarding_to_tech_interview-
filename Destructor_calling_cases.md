## There are three cases when class destructor can be called
1. When object leave visibility scope.
2. When we called destructor with delete operator.
3. When compiler handle exeption in try and stack reversing towads to catch.

## Importante notice !
For the unsuccessful created constructor destructor will not be called.
