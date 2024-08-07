# Explicit Constructor

An explicit constructor in C++ is a constructor declared with the `explicit` keyword. Its main purpose is to prevent implicit type conversions and copy-initialization. This helps avoid unintended conversions that might lead to subtle bugs or unexpected behavior.

```cpp
#include <iostream>
#include <string>

class MyString {
private:
    std::string str;

public:
    // Non-explicit constructor
    MyString(const char* s) : str(s) {
        std::cout << "Char* constructor called" << std::endl;
    }

    // Explicit constructor
    explicit MyString(int n) : str(n, 'a') {
        std::cout << "Integer constructor called" << std::endl;
    }

    void print() const {
        std::cout << str << std::endl;
    }
};

void takeMyString(const MyString& ms) {
    ms.print();
}

int main() {
    MyString s1 = "Hello";  // OK: Calls char* constructor
    s1.print();

    MyString s2(5);  // OK: Calls integer constructor
    s2.print();

    // MyString s3 = 5;  // Error: Implicit conversion not allowed
    MyString s4 = MyString(5);  // OK: Explicit conversion

    takeMyString("World");  // OK: Implicit conversion allowed
    // takeMyString(10);  // Error: Implicit conversion not allowed
    takeMyString(MyString(10));  // OK: Explicit conversion

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzzk52e).

Let's break down this example:

1. We have a `MyString` class with two constructors:
   * A non-explicit constructor that takes a `const char*`
   * An explicit constructor that takes an `int`
2. The non-explicit constructor allows implicit conversions:
   * `MyString s1 = "Hello";` works fine.
   * `takeMyString("World");` also works, implicitly converting the C-string to a `MyString`.
3. The explicit constructor prevents implicit conversions:
   * `MyString s2(5);` works as expected, calling the integer constructor.
   * `MyString s3 = 5;` would cause a compile-time error if uncommented.
   * `takeMyString(10);` would also cause an error if uncommented.
4. However, explicit conversions are still allowed:
   * `MyString s4 = MyString(5);` works fine.
   * `takeMyString(MyString(10));` is also valid.

Key points about explicit constructors:

1. They prevent implicit type conversions, reducing the risk of accidental conversions.
2. They're particularly useful for single-argument constructors to avoid unintended implicit conversions.
3. They can help catch potential errors at compile-time rather than runtime.
4. They don't prevent explicit conversions, so you can still perform the conversion when you really intend to.

Using `explicit` constructors is generally considered good practice for single-argument constructors unless you specifically want to allow implicit conversions. This can lead to more predictable and less error-prone code.
