# ✨ Heap and Stack

### Stack Memory:

1. **Automatic Memory Management**: Variables declared inside a function (local variables) are typically allocated on the stack. This includes parameters passed to functions.
2. **Scope-based Allocation**: Memory allocated on the stack is automatically deallocated when the function it belongs to returns. This makes stack allocation and deallocation very efficient.
3. **Fixed Size**: The stack size is usually fixed and limited (although this limit can be adjusted in some environments). This means that large objects or objects that require memory allocation beyond the stack size may cause stack overflow errors.
4. **Faster Access**: Accessing variables on the stack is generally faster because it involves simple pointer arithmetic.

```cpp
#include <iostream>

// Sample class definition
class MyClass {
public:
    MyClass() {
        std::cout << "MyClass constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor called" << std::endl;
    }

    void printMessage() {
        std::cout << "Hello from MyClass!" << std::endl;
    }
};

int main() {
    // Object allocated on the stack
    MyClass obj1;
    
    // Object scope limited to main function
    obj1.printMessage();

    // No need to manually deallocate stack-allocated objects
    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42m59udbt).

### Heap Memory:

1. **Manual Memory Management**: Memory allocated on the heap is not managed automatically; the programmer is responsible for allocating and deallocating memory as needed.
2. **Dynamic Allocation**: Objects created with `new` in C++ are allocated on the heap. These objects exist until explicitly deallocated with `delete`.
3. **Variable Size**: The heap can grow dynamically as memory is allocated, limited by the system's available memory.
4. **Slower Access**: Accessing variables on the heap is slower than on the stack because it involves indirection through pointers.

```cpp
#include <iostream>

// Sample class definition
class MyClass {
public:
    MyClass() {
        std::cout << "MyClass constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor called" << std::endl;
    }

    void printMessage() {
        std::cout << "Hello from MyClass!" << std::endl;
    }
};

int main() {
    // Object allocated on the heap
    MyClass *ptr = new MyClass();
    
    // Object lifetime managed manually; need to delete when done
    ptr->printMessage();

    // Explicitly deallocate heap-allocated object to avoid memory leak
    delete ptr;

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42m5avhdq).

This can be solved with scoped pointers, you can check the example here:

```cpp
#include <iostream>

// Sample class definition
class MyClass {
public:
    MyClass() {
        std::cout << "MyClass constructor called" << std::endl;
    }

    ~MyClass() {
        std::cout << "MyClass destructor called" << std::endl;
    }

    void printMessage() {
        std::cout << "Hello from MyClass!" << std::endl;
    }
};

class ScopedPtr {
private:
    MyClass* m_Ptr;
  
public:
    ScopedPtr(MyClass* ptr): m_Ptr(ptr) {}

    ~ScopedPtr() {
        delete m_Ptr;
    }

    void printMessage() {
        m_Ptr->printMessage();
    }
};

int main() {
    // Object allocated on the heap
    ScopedPtr myClass = new MyClass();
    
    // Object lifetime managed manually; need to delete when done
    myClass.printMessage();
    
    // distructor will be called autometically
    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42m5axvs8).

The above example of scoped pointer is what is done internally by a [`unique_ptr`](pointers/smart-pointers/).

### Key Differences:

* **Allocation**: Stack memory is allocated automatically and managed efficiently by the compiler, while heap memory requires explicit allocation and deallocation.
* **Lifetime**: Objects on the stack have a limited lifetime, tied to the scope they are declared in, whereas objects on the heap can persist beyond the scope where they were created.
* **Size and Limitations**: Stack size is usually limited and fixed, whereas the heap can dynamically grow based on available system memory.
* **Access**: Accessing stack variables is faster than accessing heap variables due to direct pointer manipulation versus indirection through pointers.
