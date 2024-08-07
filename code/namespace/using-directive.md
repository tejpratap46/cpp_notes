# Using directive

The `using` directive provides flexibility in how you work with namespaces, allowing you to balance between code readability and avoiding name conflicts. It's important to use these features judiciously, especially in larger codebases, to maintain clear and maintainable code.

1. `using namespace` directive:

This brings all names from a namespace into the current scope.

```cpp
#include <iostream>

namespace Math {
    int add(int a, int b) { return a + b; }
    int subtract(int a, int b) { return a - b; }
}

int main() {
    using namespace Math;
    
    // Now we can use Math functions without the Math:: prefix
    std::cout << add(5, 3) << std::endl;      // Outputs: 8
    std::cout << subtract(10, 4) << std::endl; // Outputs: 6
    
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzyx8mm).

2. `using` declaration:

This brings a specific name from a namespace into the current scope.

```cpp
#include <iostream>

namespace Math {
    int add(int a, int b) { return a + b; }
    int subtract(int a, int b) { return a - b; }
}

int main() {
    using Math::add;  // Only 'add' is brought into scope
    
    std::cout << add(5, 3) << std::endl;      // Outputs: 8
    // std::cout << subtract(10, 4) << std::endl; // This would cause an error
    std::cout << Math::subtract(10, 4) << std::endl; // This works: 6
    
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzyzu5d).

3. Namespace alias:

This creates an alternative name for a namespace, which can be useful for long namespace names.

```cpp
#include <iostream>

namespace VeryLongNamespaceName {
    void someFunction() {
        std::cout << "Function in a long namespace name" << std::endl;
    }
}

int main() {
    namespace Short = VeryLongNamespaceName;
    
    Short::someFunction();  // Outputs: Function in a long namespace name
    
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzz4bg6).

4. Inline namespace:

This is a feature where names in the inline namespace are treated as if they were part of the enclosing namespace.

```cpp
#include <iostream>

namespace Outer {
    inline namespace V1 {
        void foo() { std::cout << "V1::foo" << std::endl; }
    }
    
    namespace V2 {
        void foo() { std::cout << "V2::foo" << std::endl; }
    }
}

int main() {
    Outer::foo();     // Calls V1::foo
    Outer::V1::foo(); // Also calls V1::foo
    Outer::V2::foo(); // Calls V2::foo
    
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzz6e4z).

Important considerations:

1. Using `using namespace` in the global scope of a header file is generally considered bad practice as it can lead to name conflicts.
2. `using` declarations are often preferred over `using namespace` directives as they're more specific and less likely to cause naming conflicts.
3. Namespace aliases can improve readability when working with long namespace names.
4. Inline namespaces are often used for versioning in library design.

The `using` keyword, when used judiciously, can make code more readable and manageable when working with namespaces. However, it's important to use it carefully to avoid naming conflicts, especially in larger codebases.
