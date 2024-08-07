---
description: This is used to define macros. Macros can be simple constants or function
---

# #define

Here is an example, here defined string `PI` and `SQUARE(x)` will be replace by compiler at compile time

```cpp
#define PI 3.14159
#define SQUARE(x) ((x) * (x))

int main() {
    double radius = 5.0;
    double area = PI * SQUARE(radius);
    // ...
}
```

Here is another example

```cpp
#define MAX(a, b) ((a) > (b) ? (a) : (b))

int main() {
    int x = 5, y = 7;
    printf("Max is: %d\n", MAX(x, y));  // Output: Max is: 7
    
    // Be careful with side effects:
    printf("Max is: %d\n", MAX(x++, y++));  // This might not behave as expected
}
```

Multiline Marcos

```cpp
#define MULTI_LINE_MACRO do { \
    printf("This is a multi-line macro.\n"); \
    printf("It can contain multiple statements.\n"); \
} while(0)

int main() {
    MULTI_LINE_MACRO;
}
```
