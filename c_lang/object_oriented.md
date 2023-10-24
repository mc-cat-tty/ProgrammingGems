# Object-oriented programming in C

## Forward declaration
Used to protect access to a struct, making its attributes private.

> _object.h_
```c
typedef struct ObjName ObjName
```

> _object.c_
```c
#include "object.h"

typedef struct ObjName {
    ...  // attributes
} ObjName;
```

## Constructor
```c
ObjName OBJ_NAME(...);
```

## Methods
```c
RetVal OBJ_NAME_Method(ObjName self, ...);
```


