# 👨‍🏭 Helper function

C and C++ both have many helper functions which make it easier to work with memory, here are main ones explained:

1. new and delete operators:
   * `new`: Allocates memory for a single object
   * `delete`: Deallocates memory for a single object
   * `new[]`: Allocates memory for an array of objects
   * `delete[]`: Deallocates memory for an array of objects
2. C-style memory management functions (from \<cstdlib>):
   * `malloc()`: Allocates a block of uninitialized memory
   * `calloc()`: Allocates a block of zero-initialized memory
   * `memset()`: Fills a block of memory with a specified value.
   * `memcpy()`:Copies a block of memory from a source to a destination.
   * `realloc()`: Reallocates a previously allocated memory block
   * `free()`: Deallocates a block of memory previously allocated by malloc, calloc, or realloc
3. Smart Pointers (from \<memory>):
   * `std::unique_ptr`: For exclusive ownership of dynamically allocated memory
   * `std::shared_ptr`: For shared ownership of dynamically allocated memory
   * `std::weak_ptr`: A weak reference to an object managed by std::shared\_ptr
4. Allocator class (from \<memory>):
   * `std::allocator`: The default allocator used by standard containers
5. Other memory-related functions (from \<memory>):
   * `std::addressof()`: Obtains the actual address of an object
   * `std::align()`: Aligns pointer to the specified alignment
   * `std::uninitialized_copy()`: Copies a range of objects to uninitialized memory
   * `std::uninitialized_fill()`: Fills a range of uninitialized memory with a value
   * `std::uninitialized_move()`: Moves a range of objects to uninitialized memory
   * `std::destroy()`: Destroys objects in a range
6. C++17 additions:
   * `std::launder()`: Helps deal with object lifetime issues in certain scenarios
7. C++20 additions:
   * `std::make_unique_for_overwrite()`: Creates a unique\_ptr without value-initializing its contents
   * `std::make_shared_for_overwrite()`: Creates a shared\_ptr without value-initializing its contents
8. Placement new:
   * `new (place_address) type`: Constructs an object at a specific memory address

It's worth noting that in modern C++, direct use of low-level memory management functions like malloc() and free() is generally discouraged in favor of C++-style memory management (new/delete) or, even better, smart pointers and standard containers.

The smart pointers (unique\_ptr, shared\_ptr, weak\_ptr) are particularly important as they help manage memory automatically and prevent common issues like memory leaks and dangling pointers.

Example:

```cpp
#include <iostream>
#include <cstdlib>
#include <memory>
#include <vector>
#include <cstring>

class MyClass {
public:
    MyClass() { std::cout << "MyClass constructed\n"; }
    ~MyClass() { std::cout << "MyClass destructed\n"; }
};

int main() {
    // 1. new and delete operators
    std::cout << "1. new and delete operators:\n";
    MyClass* ptr = new MyClass();
    delete ptr;

    int* arr = new int[5];
    delete[] arr;

    // 2. C-style memory management
    std::cout << "\n2. C-style memory management:\n";
    int* c_ptr = (int*)malloc(sizeof(int));
    *c_ptr = 10;
    std::cout << "malloc: " << *c_ptr << std::endl;
    free(c_ptr);

    int* c_arr = (int*)calloc(5, sizeof(int));
    std::cout << "calloc: " << c_arr[0] << std::endl;  // Will be 0
    c_arr = (int*)realloc(c_arr, 10 * sizeof(int));
    free(c_arr);
    
    // memset with integers (be cautious!)
    int numbers[5] = {1, 2, 3, 4, 5};
    std::cout << "\nBefore memset: ";
    for (int i = 0; i < 5; ++i) std::cout << numbers[i] << " ";
    std::cout << std::endl;
    
    memset(numbers, 0, sizeof(numbers));
    std::cout << "After memset:  ";
    for (int i = 0; i < 5; ++i) std::cout << numbers[i] << " ";
    std::cout << std::endl;
    
    std::cout << "\nmemcpy example:\n";
    char srcMemCpy[] = "Hello, memcpy!";
    char destMemCpy[20];
    
    memcpy(destMemCpy, src, strlen(srcMemCpy) + 1);  // +1 to include null terminator
    std::cout << "Source: " << srcMemCpy << std::endl;
    std::cout << "Destination: " << destMemCpy << std::endl;

    // 3. Smart Pointers
    std::cout << "\n3. Smart Pointers:\n";
    std::unique_ptr<MyClass> uptr = std::make_unique<MyClass>();
    std::shared_ptr<MyClass> sptr = std::make_shared<MyClass>();
    std::weak_ptr<MyClass> wptr = sptr;

    // 4. Allocator
    std::cout << "\n4. Allocator:\n";
    std::allocator<int> alloc;
    int* alloc_ptr = alloc.allocate(1);
    alloc.construct(alloc_ptr, 42);
    std::cout << "Allocator: " << *alloc_ptr << std::endl;
    alloc.destroy(alloc_ptr);
    alloc.deallocate(alloc_ptr, 1);

    // 5. Other memory-related functions
    std::cout << "\n5. Other memory-related functions:\n";
    int x = 10;
    int* addr = std::addressof(x);
    std::cout << "addressof: " << addr << std::endl;

    std::vector<int> src = {1, 2, 3, 4, 5};
    std::vector<int> dest(5);
    std::uninitialized_copy(src.begin(), src.end(), dest.begin());
    std::cout << "uninitialized_copy: " << dest[2] << std::endl;

    // 6. C++17 std::launder (usage is advanced and situational)
    // Example omitted due to its specialized nature

    // 7. C++20 additions
    #if __cplusplus >= 202002L
    std::cout << "\n7. C++20 additions:\n";
    auto uptr_overwrite = std::make_unique_for_overwrite<int>();
    auto sptr_overwrite = std::make_shared_for_overwrite<int>();
    #endif

    // 8. Placement new
    std::cout << "\n8. Placement new:\n";
    char memory[sizeof(MyClass)];
    MyClass* placed_ptr = new (memory) MyClass();
    placed_ptr->~MyClass();  // Call destructor manually

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42m3u27ts).
