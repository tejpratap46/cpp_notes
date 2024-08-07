# Dangling Pointer

A **dangling pointer** is a pointer that points to a memory location that has been deallocated or freed. This means the memory it once pointed to no longer exists, and the pointer is left "dangling."

#### How Dangling Pointers Occur

There are primarily three ways a dangling pointer can arise:

1. **Deallocation of memory:**
   * When you use `delete` or `free` to deallocate memory, the pointer still holds the address of the freed memory.
   * If you subsequently try to access or modify the memory through this pointer, you'll invoke undefined behavior, leading to crashes or corrupted data.
2. **Local variable going out of scope:**
   * When a function returns, local variables within that function go out of scope.
   * If you return the address of a local variable, the pointer becomes dangling once the function ends.
   * Accessing this pointer outside the function's scope is invalid.
3. **Object deletion:**
   * When an object is deleted using `delete`, the pointer to that object becomes dangling.
   * Continuing to use the pointer after deletion results in undefined behavior.

#### Example

```cpp
#include <iostream>

int* dangerousFunction() {
    int x = 10;
    return &x; // Returning the address of a local variable
}

int main() {
    int* ptr = dangerousFunction();
    std::cout << *ptr << std::endl; // Undefined behavior!
    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42n95nsew).

Use code with caution.

In this example, `ptr` becomes a dangling pointer because it points to the address of `x`, which is a local variable. Once `dangerousFunction` returns, `x` goes out of scope, and accessing `*ptr` leads to undefined behavior.

#### Consequences of Dangling Pointers

* **Undefined behavior:** The program's behavior is unpredictable, and it might crash or produce incorrect results.
* **Memory corruption:** Trying to access or modify memory through a dangling pointer can corrupt other data.
* **Security vulnerabilities:** Exploiting dangling pointers can lead to security vulnerabilities.

#### Preventing Dangling Pointers

* **Nulling the pointer:** After deallocating memory, set the pointer to `nullptr`.
* **Avoiding returning addresses of local variables:** Use references or output parameters instead.
* **Smart pointers:** C++11 introduced smart pointers (like `unique_ptr`, `shared_ptr`) that automatically manage memory, reducing the risk of dangling pointers.
* **Careful memory management:** Be mindful of when and how memory is allocated and deallocated.
