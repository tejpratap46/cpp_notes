# Unique Pointer

They automatically delete the pointed-to object when it's no longer needed, i.e. it goes out of scope.

Key points about `std::unique_ptr`:

* It's a smart pointer that owns and manages another object through a pointer and disposes of that object when the `unique_ptr` goes out of scope.
* It cannot be copied, only moved, ensuring single ownership.
* Use std::make\_unique to create a `unique_ptr` (C++14 onwards).
* Automatically calls delete on the managed object when going out of scope.
* Move to contained value (pointer) to another `unique_ptr` using `std::move(ptr1)`

Example:

```cpp
#include <iostream>
#include <memory>

class Resource {
public:
    Resource() { std::cout << "Resource acquired\n"; }
    ~Resource() { std::cout << "Resource destroyed\n"; }
    void use() { std::cout << "Resource used\n"; }
};

int main() {
    // Create a unique_ptr
    std::unique_ptr<Resource> ptr1 = std::make_unique<Resource>();
    // Copy constructor is not allowed.
    // std::unique_ptr<Resource> ptr2 = ptr1; // Not allowed
    
    // Use the managed object
    ptr1->use();
    
    // Transfer ownership
    std::unique_ptr<Resource> ptr2 = std::move(ptr1);
    
    // ptr1 is now nullptr
    if (ptr1 == nullptr) {
        std::cout << "ptr1 is null\n";
    }
    
    // ptr2 now owns the Resource
    ptr2->use();
    
    // Resource is automatically deleted when ptr2 goes out of scope
    return 0;
}
```
