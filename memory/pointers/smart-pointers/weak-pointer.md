# Weak Pointer

Weak pointers in C++ are smart pointers that hold a non-owning ("weak") reference to an object that is managed by a shared pointer. They are used to break circular references between shared pointers and to observe an object without affecting its lifetime. Unlike shared pointers, weak pointers don't increment the reference count of the object they point to.

Here's a simple example to demonstrate the use of weak pointers:

```cpp
#include <iostream>
#include <memory>

class Person {
public:
    Person(const std::string& name) : name_(name) {
        std::cout << name_ << " created" << std::endl;
    }
    ~Person() {
        std::cout << name_ << " destroyed" << std::endl;
    }
    void greet() {
        std::cout << "Hello, I'm " << name_ << std::endl;
    }

private:
    std::string name_;
};

int main() {
    // Create a shared pointer
    std::shared_ptr<Person> shared = std::make_shared<Person>("Alice");
    
    // Create a weak pointer from the shared pointer
    std::weak_ptr<Person> weak = shared;
    
    // Use the weak pointer
    if (auto temp = weak.lock()) {
        temp->greet();
    } else {
        std::cout << "Object no longer exists" << std::endl;
    }
    
    // Reset the shared pointer ref counter
    // i.e. release all weak pointers references
    shared.reset();
    
    // Try to use the weak pointer again
    if (auto temp = weak.lock()) {
        temp->greet();
    } else {
        std::cout << "Object no longer exists" << std::endl;
    }
    
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42n8tg7nb).

Key points in this example:

1. We define a simple `Person` class with a constructor, destructor, and a `greet()` method.
2. In `main()`, we create a `shared_ptr<Person>` named `shared`.
3. We then create a `weak_ptr<Person>` named `weak` from the `shared` pointer.
4. To use the weak pointer, we need to call its `lock()` method, which returns a `shared_ptr`. If the object still exists, we can use it; otherwise, `lock()` returns a null pointer.
5. After resetting the `shared` pointer, the `Person` object is destroyed because there are no more `shared_ptr`s pointing to it.
6. When we try to use the weak pointer again, `lock()` returns a null pointer, showing that the object no longer exists.
