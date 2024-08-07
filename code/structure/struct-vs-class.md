# Struct vs Class

tldr. both are almost similar with default visibility of data and functions being public in `Struct` and private in `Class`.

key differences:

1. Default Access Specifier:
   * In a class, members are private by default.
   * In a struct, members are public by default.
2. Inheritance:
   * For a class, the default inheritance is private.
   * For a struct, the default inheritance is public.
3. Purpose and Convention:
   * Classes are typically used for objects with both data and methods, often implementing data hiding.
   * Structs are conventionally used for passive objects with public data and few or no methods.
4. Functionality:
   * Functionally, classes and structs are almost identical in C++.
   * You can add methods, constructors, and use inheritance with both.

Here's a brief example to illustrate these differences:

```cpp
struct MyStruct {
    int x;  // public by default
    void print() { std::cout << x << std::endl; }
};

class MyClass {
    int x;  // private by default
public:
    void print() { std::cout << x << std::endl; }
};

int main() {
    MyStruct s;
    s.x = 5;  // OK, x is public

    MyClass c;
    // c.x = 5;  // Error, x is private
    
    return 0;
}
```

In this example:

* The struct's member `x` is accessible directly.
* The class's member `x` is private and not accessible outside the class.

Inheritance example:

```cpp
struct BaseStruct {};
struct DerivedStruct : BaseStruct {};  // public inheritance by default

class BaseClass {};
class DerivedClass : BaseClass {};  // private inheritance by default
```

It's worth noting that in practice, the choice between struct and class often comes down to coding style and convention rather than functionality. Many C++ programmers use structs for simple data structures and classes for more complex objects with behavior.
