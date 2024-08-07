# 🎯 Pointers

Pointers in C++ are variables that store memory addresses. They're a powerful feature that allows for efficient memory management and manipulation.

*   Basic Concept: A pointer holds the memory address of another variable.

    ```cpp
    int x = 10;
    int* ptr = &x;  // ptr now holds the address of x
    ```
*   Declaration: Syntax is: `type* pointer_name;`

    ```cpp
    int* intPtr;
    double* doublePtr;
    char* charPtr;
    ```
*   Initialization: Use the address-of operator (&) to get a variable's address.

    ```cpp
    int y = 20;
    int* yPtr = &y;
    ```
*   Dereferencing: Use the dereference operator (\*) to access the value at the address.

    ```cpp
    int z = *yPtr;  // z now equals 20
    ```
*   Pointer Arithmetic: You can perform arithmetic on pointers.

    ```cpp
    int arr[] = {10, 20, 30, 40};
    int* arrPtr = arr;

    std::cout << *arrPtr;     // Prints 10
    std::cout << *(arrPtr+1); // Prints 20
    ```
*   Null Pointers: Pointers can be set to null to indicate they don't point to any valid memory.

    ```cpp
    int* nullPtr = nullptr;  // Modern C++ (C++11 and later)
    int* nullPtr = NULL;     // C-style null pointer (older code)
    ```
*   Pointers and Arrays: Array names decay to pointers to their first elements.

    ```cpp
    int numbers[] = {1, 2, 3, 4, 5};
    int* numPtr = numbers;  // numPtr points to the first element
    ```
*   Pointers to Functions: You can have pointers to functions, useful for callbacks.

    ```cpp
    int add(int a, int b) { return a + b; }
    int (*funcPtr)(int, int) = add;
    int result = funcPtr(5, 3);  // result is 8
    ```
*   Dynamic Memory Allocation: Pointers are crucial for dynamic memory management.

    ```cpp
    int* dynamicInt = new int(42);
    delete dynamicInt;  // Don't forget to free the memory
    ```
*   Const Pointers: You can have constant pointers or pointers to constants.

    ```cpp
    int x = 10;
    const int* ptr1 = &x;  // Pointer to constant int
    int* const ptr2 = &x;  // Constant pointer to int
    const int* const ptr3 = &x;  // Constant pointer to constant int
    ```

Example:

```cpp
#include <iostream>

int main() {
    int x = 10;
    int* ptr = &x;

    std::cout << "Value of x: " << x << std::endl;
    std::cout << "Address of x: " << ptr << std::endl;
    std::cout << "Value pointed to by ptr: " << *ptr << std::endl;

    *ptr = 20;  // Modify x through the pointer
    std::cout << "New value of x: " << x << std::endl;

    return 0;
}
```
