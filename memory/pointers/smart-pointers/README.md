# Smart Pointers

Smart pointers are a feature in C++ that help manage dynamic memory allocation and deallocation, providing better memory safety and reducing the risk of memory leaks and dangling pointers. They are objects that act like pointers but offer additional functionality, primarily automatic memory management.

Let's go through the main types of smart pointers in C++:

1. std::unique\_ptr
2. std::shared\_ptr
3. std::weak\_ptr

```cpp
#include <iostream>
#include <memory>

class Resource {
public:
    Resource(int value) : data(value) {
        std::cout << "Resource acquired: " << data << std::endl;
    }
    ~Resource() {
        std::cout << "Resource destroyed: " << data << std::endl;
    }
    void use() {
        std::cout << "Using resource: " << data << std::endl;
    }
private:
    int data;
};

void uniquePtrExample() {
    std::cout << "unique_ptr example:" << std::endl;
    std::unique_ptr<Resource> uniqueRes = std::make_unique<Resource>(1);
    uniqueRes->use();
    // uniqueRes will be automatically deleted when it goes out of scope
}

void sharedPtrExample() {
    std::cout << "\nshared_ptr example:" << std::endl;
    std::shared_ptr<Resource> sharedRes1 = std::make_shared<Resource>(2);
    {
        std::shared_ptr<Resource> sharedRes2 = sharedRes1;
        std::cout << "Resource count: " << sharedRes1.use_count() << std::endl;
        sharedRes2->use();
    }
    std::cout << "Resource count after inner scope: " << sharedRes1.use_count() << std::endl;
    // sharedRes1 will be deleted when the last shared_ptr goes out of scope
}

void weakPtrExample() {
    std::cout << "\nweak_ptr example:" << std::endl;
    std::shared_ptr<Resource> sharedRes = std::make_shared<Resource>(3);
    std::weak_ptr<Resource> weakRes = sharedRes;
    
    if (auto tempShared = weakRes.lock()) {
        tempShared->use();
    } else {
        std::cout << "Resource no longer available" << std::endl;
    }
    
    sharedRes.reset();  // Explicitly release the resource
    
    if (auto tempShared = weakRes.lock()) {
        tempShared->use();
    } else {
        std::cout << "Resource no longer available" << std::endl;
    }
}

int main() {
    uniquePtrExample();
    sharedPtrExample();
    weakPtrExample();
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzwqw3h).

Now, let's break down each type of smart pointer:

1. std::unique\_ptr
   * Owns and manages another object through a pointer and disposes of that object when the unique\_ptr goes out of scope.
   * Cannot be copied, ensuring single ownership.
   * Can be moved to transfer ownership.
   * Use when you need exclusive ownership of a resource.
2. std::shared\_ptr
   * Retains shared ownership of an object through a pointer.
   * Several shared\_ptr objects may own the same object.
   * The object is destroyed when the last remaining shared\_ptr owning it is destroyed.
   * Has a control block that keeps track of the number of shared\_ptr instances sharing ownership.
   * Use when you need to share ownership of a resource.
3. std::weak\_ptr
   * Holds a non-owning ("weak") reference to an object that is managed by std::shared\_ptr.
   * Must be converted to std::shared\_ptr to access the referenced object.
   * Can be used to break circular references of shared\_ptr.
   * Use when you want to observe an object but don't require it to remain alive.

Key benefits of using smart pointers:

1. Automatic memory management: They automatically delete the pointed-to object when it's no longer needed.
2. Exception safety: They ensure resources are properly released if an exception occurs.
3. Clear ownership semantics: They make the ownership of dynamically allocated objects explicit.
4. Prevention of common pointer errors: They help avoid issues like dangling pointers and memory leaks.
