# Other constructors

In C++, we have 9 types of constructors, including copy and explicit constructor, here is a gist of all type of constructors.

```cpp
#include <iostream>
using namespace std;

class Example {
public:
    // 1. Default Constructor
    Example()
    {
        cout << "Initialize members with default values" << endl;
    }

    // 2. Parameterized Constructor
    Example(int a, double b) : member_a(a), member_b(b)
    {
        cout << "Initialize members with provided values" << endl;
    }

    // 3. Copy Constructor
    Example(const Example &other) : member_a(other.member_a), member_b(other.member_b)
    {
        cout << "Create a new object as a copy of an existing object" << endl;
    }

    // 4. Move Constructor
    Example(Example &&other) noexcept
        : member_a(std::move(other.member_a)), member_b(std::move(other.member_b))
    {
        cout << "Transfer ownership of resources from one object to another" << endl;
    }

    // 5. Delegating Constructor
    Example(int a) : Example(a, 0.0)
    {
        cout << "Delegate to the two-parameter constructor" << endl;
    }

    // 6. Converting Constructor
    explicit Example(double d) : member_a(static_cast<int>(d)), member_b(d)
    {
        cout << "Convert from another type (in this case, double)" << endl;
    }

    // 7. Copy-List-Initialization Constructor
    Example(std::initializer_list<int> list)
    {
        cout << "Initialize from a list of values" << endl;
    }

private:
    int member_a;
    double member_b;
};

int main() {

    // Usage examples:
    Example e1;                 // Default constructor
    Example e2(10, 3.14);       // Parameterized constructor
    Example e3 = e2;            // Copy constructor
    Example e4 = std::move(e3); // Move constructor
    Example e5(5);              // Delegating constructor
    Example e6 = Example(3.14); // Converting constructor
    Example e7 = {1, 2, 3, 4};  // Copy-list-initialization constructor
    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42nfmf96r).

Lets take a look at each one.

1. Default Constructor:
   * Takes no parameters
   * Called when an object is created without arguments
   * If not explicitly defined and no other constructors are present, the compiler provides one
2. Parameterized Constructor:
   * Takes one or more parameters
   * Allows customization of object initialization
3. Copy Constructor:
   * Creates a new object as a copy of an existing object
   * Takes a const reference to an object of the same class as a parameter
   * Called when an object is passed by value, returned by value, or explicitly copied
4. Move Constructor:
   * Transfers ownership of resources from one object to another
   * Takes an rvalue reference (&&) as a parameter
   * Typically used for optimizing resource management, especially for large objects
5. Delegating Constructor:
   * Calls another constructor in the same class to perform initialization
   * Helps reduce code duplication in constructors
6. Converting Constructor:
   * Allows implicit or explicit conversion from other types
   * Often declared with the 'explicit' keyword to prevent unintended implicit conversions
7. Copy-List-Initialization Constructor:
   * Takes an std::initializer\_list as a parameter
   * Allows initialization of an object with a list of values

Additionally, there are a few other constructor-related concepts:

8.  Explicitly Defaulted and Deleted Constructors:

    ```cpp
    Example() = default;  // Explicitly defaulted
    Example(const Example&) = delete;  // Explicitly deleted
    ```

    * Allows explicit control over compiler-generated special member functions
9.  In-Class Member Initializers:

    ```cpp
    class Example {
        int x = 0;  // In-class initializer
    public:
        Example() {}  // x is initialized to 0
        Example(int val) : x(val) {}  // x is initialized to val
    };
    ```

    * Provides default values for members, used when not explicitly initialized in a constructor

These different types of constructors provide flexibility in object creation and initialization, allowing for efficient and clear code in various scenarios. The choice of which constructors to implement depends on the specific needs of your class and how it will be used.
