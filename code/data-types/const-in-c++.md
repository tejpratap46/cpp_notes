# const in c++

Similar to `final` in Java, we can declare a const variable in cpp, which will than be immutable.

#### What if i use pointer to change directly on memory?

In C++, when you declare a variable as const, you're promising not to modify its value through that particular name. However, there's a way to circumvent this protection using pointers, though it's considered bad practice and can lead to undefined behavior.

Example:

1. Direct modification: This is not allowed.

```cpp
const int x = 5;
x = 10;  // Compilation error
```

2. Modification through a non-const pointer: This is possible, but it's undefined behavior.

```cpp
const int x = 5;
int* ptr = const_cast<int*>(&x);
*ptr = 10;  // Compiles, but is undefined behavior
```

In this case, the code will compile, but it's not guaranteed to work as expected. The behavior is undefined because:

* The compiler might optimize away the modification, assuming x is truly const.
* x might be stored in read-only memory.
* It violates the const contract, potentially leading to unexpected results.

3.  Modification of const data through a pointer to non-const:

    ```cpp
    int y = 5;
    const int* ptr = &y;
    // *ptr = 10;  // Compilation error
    y = 10;  // This is allowed
    ```

Here, ptr is a pointer to const int, meaning you can't modify the value through ptr, but you can still modify y directly.

It's important to note that while it's technically possible to modify a const variable using pointers and const\_cast, doing so is considered very bad practice and should be avoided. It defeats the purpose of const-correctness and can lead to difficult-to-debug issues.
