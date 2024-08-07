# 🕵️ Header File

In cpp, header files are used at compile time to resolve references, share common code and declare variables.

Example:

```cpp
// math_operations.h
#ifndef MATH_OPERATIONS_H
#define MATH_OPERATIONS_H

int add(int a, int b);
int subtract(int a, int b);

#endif
```

```cpp
// math_operations.c
#include "math_operations.h

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}
```

```cpp
// main.c
#include <stdio.h>
#include "math_operations.h"

int main() {
    printf("5 + 3 = %d\n", add(5, 3));
    printf("5 - 3 = %d\n", subtract(5, 3));
    return 0;
}
```
