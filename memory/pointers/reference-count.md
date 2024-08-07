# Reference count

Reference count in c++ helps program to keep track of pointer usage and delete it from memory when it is no longer needed.

You can read different methods to use reference counts on you program using smart pointers in following pages:

1. [unique-pointer.md](smart-pointers/unique-pointer.md "mention")
2. [shared-pointer.md](smart-pointers/shared-pointer.md "mention")
3. [weak-pointer.md](smart-pointers/weak-pointer.md "mention")

You can check how to get count of reference in each of the smart pointer using below code snippet:

```cpp
#include <iostream>
#include <memory>

class MyClass {
public:
    MyClass() { std::cout << "MyClass constructed\n"; }
    ~MyClass() { std::cout << "MyClass destructed\n"; }
};

int main() {
    // Create a shared pointer
    std::shared_ptr<MyClass> ptr1 = std::make_shared<MyClass>();
    std::cout << "Reference count after ptr1 creation: " << ptr1.use_count() << std::endl;

    // Create another shared pointer pointing to the same object
    std::shared_ptr<MyClass> ptr2 = ptr1;
    std::cout << "Reference count after ptr2 creation: " << ptr1.use_count() << std::endl;

    // Create a weak pointer
    std::weak_ptr<MyClass> weak = ptr1;
    std::cout << "Reference count after weak ptr creation: " << ptr1.use_count() << std::endl;

    // Reset ptr2
    ptr2.reset();
    std::cout << "Reference count after ptr2 reset: " << ptr1.use_count() << std::endl;

    // Reset ptr1
    ptr1.reset();
    std::cout << "Reference count after ptr1 reset: " << (weak.expired() ? 0 : weak.lock().use_count()) << std::endl;

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42n8thtfp).

The output of this program would look something like this:

```
MyClass constructed
Reference count after ptr1 creation: 1
Reference count after ptr2 creation: 2
Reference count after weak ptr creation: 2
Reference count after ptr2 reset: 1
MyClass destructed
Reference count after ptr1 reset: 0
```

Key points in this example:

1. We define a simple `MyClass` with a constructor and destructor that print messages when they're called.
2. We use `std::make_shared<MyClass>()` to create a `shared_ptr` named `ptr1`.
3. We use the `use_count()` member function to get the current reference count of the shared pointer.
4. We create another shared pointer `ptr2` that points to the same object as `ptr1`. This increases the reference count.
5. We create a weak pointer `weak` from `ptr1`. This does not increase the reference count.
6. We reset `ptr2`, which decreases the reference count.
7. Finally, we reset `ptr1`. At this point, the object is destroyed because there are no more shared pointers pointing to it.
8. For the last count, we use `weak.expired()` to check if the object still exists, and if it does, we use `weak.lock().use_count()` to get the count. If the object no longer exists, we print 0.

It's important to note that while `use_count()` is useful for understanding and debugging shared pointer behavior, you shouldn't rely on it for program logic, as its exact behavior can vary between implementations.
