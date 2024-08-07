# Copy Constructor

A copy constructor in C++ is a special constructor that creates a new object as a copy of an existing object. It's used in several scenarios:

1. When an object is passed by value to a function.

```cpp
void func(MyClass a) {
}

int main() {
  MyClass myClass;
   // below, a shallow copy of myClass is created and supplied to func(MyClass a)
  func(myClass);
  return 0;
}
```

2. When a function returns an object by value

```cpp
MyClass func() {
  MyClass myClass;
  // below, a shallow copy of myClass is created and supplied back to caller, i.e. main()
  return myClass;
}

int main() {
  MyClass myClass = func();
  return 0;
}
```

3. When an object is initialized with another object of the same class

```cpp
int main() {
  MyClass myClass;
  // below, a shallow copy of myClass is created and set to caller
  MyClass myClass2 = myClass;
  return 0;
}
```

4. When the compiler generates a temporary object

```cpp
void takeConstRef(const MyClass& obj) {}

takeConstRef(MyClass(20));  // Temporary object created and bound to const reference
```

#### Example:

```cpp
#include <iostream>
#include <cstring>

class String {
private:
    char* data;
    size_t length;

public:
    // Constructor
    String(const char* str = nullptr) {
        if (str == nullptr) {
            data = new char[1];
            data[0] = '\0';
            length = 0;
        } else {
            length = strlen(str);
            data = new char[length + 1];
            strcpy(data, str);
        }
    }

    // See what will happen if you remove below Copy constructor
    // Copy constructor
    String(const String& other) {
        length = other.length;
        data = new char[length + 1];
        strcpy(data, other.data);
    }

    // Destructor
    ~String() {
        delete[] data;
    }

    // For demonstration purposes
    void print() const {
        std::cout << data << std::endl;
    }
};

int main() {
    String s1("Hello");
    String s2 = s1;  // Copy constructor is called

    s1.print();  // Output: Hello
    s2.print();  // Output: Hello

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42m6pmq5g).

In above example, here is what's happening:

1. We created simple implementation of `String` class.
2. As data members, we have a `char* data` which will hold pointer to memory location of our char array `"Hello"`.
3. When we reassign our `String s2` to `s1`, compiler will create a shallow copy of `s1`, which means, it will set `const* data` of `s2` to same memory location if `s1`'s `*data` pointer. I.e. both the objects will point to same memory location.
4. As `String s1` and `String s2` both were created using [stack](../../memory/heap-and-stack.md#stack-memory) will be removed when our main function scope is done.
5. First `s1`'s destructor will be called, destructor will free memory of string `"Hello"`, i.e. memory at pointer location `*data` will be freed.
6. Now when `s2`'s destructor is called, which will try to free memory at location `*data`, which has been already removed by `s1`'s destructor, as both `*data` was pointing to same memory location.
7. As the memory location pointed by `*data` is already free and no longer part of your application, it cannot be made free.
8. Hence, your program will exit with compiler saying that this app tried to call free twice on a memory location Or kernel will shout that you tried to access something you do not own.

#### Key points about copy constructors:

1. Syntax: They take a const reference to an object of the same class as a parameter.
2. Default behaviour: If you don't define a copy constructor, the compiler provides a default one that performs a shallow copy (member-wise copy).
3. Deep vs. Shallow Copy: For classes with dynamically allocated resources, you often need to define a copy constructor to perform a deep copy, ensuring each object has its own independent copy of the resources.
4. Rule of Three/Five: If you define a copy constructor, you typically also need to define a destructor and a copy assignment operator (Rule of Three). In modern C++, you might also include a move constructor and move assignment operator (Rule of Five).
5.  Prevention: You can prevent copying by declaring the copy constructor as `delete`:

    ```cpp
    String(const String& other) = delete;
    ```
6. Performance: For large objects, passing by reference is often more efficient than passing by value to avoid unnecessary copying.

Copy constructors are crucial for proper resource management and preventing issues like double deletion or unintended shared state between objects, especially when dealing with dynamically allocated memory or other resources.
