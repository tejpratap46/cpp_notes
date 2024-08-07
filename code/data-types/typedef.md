# TypeDef

Typedef in C++ is a keyword used to create aliases or alternative names for existing data types. It's a way to simplify complex type declarations and make code more readable.

1.  Basic Syntax:

    ```cpp
    typedef existing_type new_type_name;
    ```
2.  Simple Example:

    ```cpp
    typedef unsigned long ulong;
    ulong myNumber = 1000000UL;
    ```
3.  Array Typedef:

    ```cpp
    typedef int IntArray[5];
    IntArray myArray = {1, 2, 3, 4, 5};
    ```
4.  Pointer Typedef:

    ```cpp
    typedef int* IntPtr;
    IntPtr ptr = new int(10);
    ```
5.  Function Pointer Typedef:

    ```cpp
    typedef int (*MathFunc)(int, int);
    int add(int a, int b) { return a + b; }
    MathFunc operation = add;
    ```
6.  Struct Typedef:

    ```cpp
    typedef struct {
        int x;
        int y;
    } Point;

    Point p = {10, 20};
    ```
7.  Complex Types:

    ```cpp
    typedef std::vector<std::pair<std::string, int>> NameScorePairs;
    NameScorePairs scores;
    ```
8.  Template Typedef (C++11 and later):

    ```cpp
    template<typename T>
    using Vec = std::vector<T>;

    Vec<int> numbers = {1, 2, 3, 4, 5};
    ```
9.  Improving Readability:

    ```cpp
    typedef std::unique_ptr<MyClass> MyClassPtr;
    MyClassPtr ptr = std::make_unique<MyClass>();
    ```
10. Portability:

    ```cpp
    typedef long long int64;  // Ensures 64-bit integer across platforms
    ```

Example:

```cpp
#include <iostream>
#include <vector>
#include <string>

// Simple typedef
typedef unsigned int uint;

// Function pointer typedef
typedef int (*Operation)(int, int);

// Struct typedef
typedef struct {
    std::string name;
    int age;
} Person;

// Complex type typedef
typedef std::vector<std::pair<std::string, int>> ScoreBoard;

// Function to use with function pointer
int add(int a, int b) {
    return a + b;
}

int main() {
    uint number = 42;
    std::cout << "Number: " << number << std::endl;

    Operation op = add;
    std::cout << "10 + 20 = " << op(10, 20) << std::endl;

    Person alice = {"Alice", 30};
    std::cout << alice.name << " is " << alice.age << " years old." << std::endl;

    ScoreBoard scores = {{"Bob", 95}, {"Charlie", 88}};
    for (const auto& score : scores) {
        std::cout << score.first << " scored " << score.second << std::endl;
    }

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzy8g6g).

Key points about typedef:

* It doesn't create a new type; it just introduces a new name for an existing type.
* It can make complex declarations more readable.
* It's often used to create platform-independent type definitions.
* In modern C++ (C++11 and later), the `using` keyword can be used similarly to typedef and is more flexible, especially with templates.
