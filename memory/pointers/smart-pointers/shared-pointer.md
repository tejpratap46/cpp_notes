# Shared Pointer

As we saw, unique pointer are one-to-one mapped. Meaning, one pointer variable can only stored by one `unique_prt` and it cannot be referenced by any other unique pointer. A unique pointer will free the referenced memory as soon as this `unique_ptr` goes out of scope.

A `shared_ptr` is different from that, here you can create multiple wrappers that are refer to same pointer, memory will be freed once all the `shared_ptr` goes out of scope.



Shared pointers are a type of smart pointer introduced in C++11 that provide automatic memory management through reference counting. Here's a concise overview:

Shared pointers (`std::shared_ptr`) allow multiple pointers to share ownership of a dynamically allocated object. Key points:

1. Automatic memory management: The object is automatically deleted when the last shared pointer owning it is destroyed.
2. Reference counting: Internally maintains a count of how many shared pointers are pointing to the object.
3. Thread-safe reference count: The reference count is incremented and decremented in a thread-safe manner.
4. Overhead: Slight performance overhead due to reference counting.
5. Cyclic references: Can lead to memory leaks if not handled properly (use weak\_ptr to break cycles).

```cpp
#include <memory>
#include <iostream>

class MyClass {
public:
    MyClass() { std::cout << "MyClass constructed\n"; }
    ~MyClass() { std::cout << "MyClass destructed\n"; }
};

int main() {
    {
        std::shared_ptr<MyClass> ptr1 = std::make_shared<MyClass>();
        {
            std::shared_ptr<MyClass> ptr2 = ptr1; // Share ownership
            std::cout << "Count: " << ptr1.use_count() << std::endl; // Prints 2
        }
        std::cout << "Count: " << ptr1.use_count() << std::endl; // Prints 1
    }
    // MyClass object is automatically deleted here
    return 0;
}
```
