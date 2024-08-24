# Move Semantics

As read before, move semantics in cpp is nothing but working with something temporary and moving (pointing) it to some other variable to keep this data alive.

> Note: temperary is denoted as `&&` in a cpp program.

Here is an example:

```cpp
#include <iostream>
#include <cstring>

class MyString {
private:
    char* data;
    size_t length;

public:
    // Constructor
    MyString(const char* str) {
        length = strlen(str);
        data = new char[length + 1];
        strcpy(data, str);
    }

    // Destructor
    ~MyString() {
        delete[] data;
    }

    // Copy constructor
    MyString(const MyString& other) {
        length = other.length;
        data = new char[length + 1];
        strcpy(data, other.data);
        std::cout << "Copy constructor called" << std::endl;
    }

    // Move constructor
    MyString(MyString&& other) noexcept {
        data = other.data;
        length = other.length;
        other.data = nullptr;
        other.length = 0;
        std::cout << "Move constructor called" << std::endl;
    }

    // Copy assignment operator
    MyString& operator=(const MyString& other) {
        if (this != &other) {
            delete[] data;
            length = other.length;
            data = new char[length + 1];
            strcpy(data, other.data);
        }
        std::cout << "Copy assignment called" << std::endl;
        return *this;
    }

    // Move assignment operator
    MyString& operator=(MyString&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            length = other.length;
            other.data = nullptr;
            other.length = 0;
        }
        std::cout << "Move assignment called" << std::endl;
        return *this;
    }

    // Function to get string length
    size_t size() const {
        return length;
    }
};

// Function that returns a MyString object
MyString createString() {
    return MyString("Temporary String");
}

int main() {
    MyString str1("Hello");
    MyString str2 = str1;  // Copy construction
    MyString str3 = std::move(str1);  // Move construction

    MyString str4("World");
    str4 = str2;  // Copy assignment
    str4 = createString();  // Move assignment

    return 0;
}
```

Let me explain the key points of this example:

1. We've defined a `MyString` class with both copy and move semantics.
2. Copy operations (constructor and assignment) create a new buffer and copy the data.
3. Move operations (constructor and assignment) transfer ownership of the buffer without copying data.
4. In the `main()` function:
   * `str2 = str1` uses copy construction
   * `str3 = std::move(str1)` uses move construction
   * `str4 = str2` uses copy assignment
   * `str4 = createString()` uses move assignment (because `createString()` returns a temporary)
5. The move operations are more efficient because they avoid allocating new memory and copying data. Instead, they simply transfer ownership of the existing data.
6. After a move operation, the source object (`str1` in the move construction case) is left in a valid but unspecified state. In this implementation, we set its pointer to `nullptr` and length to 0.
7. The `noexcept` specifier on move operations is a guarantee that these operations won't throw exceptions, which allows for further optimizations by the compiler.

When you run this program, you'll see which constructors and assignment operators are called in each case. The move operations will be used for temporary objects (like the one returned by `createString()`), resulting in better performance.

This example demonstrates how move semantics can improve efficiency by avoiding unnecessary copying, especially when dealing with temporary objects or explicitly using `std::move`.
