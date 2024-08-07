# const function vs final function

cpp supports `const` and `final` both are supported as function type, here is the main differene between them:

```cpp
#include <iostream>

class Base {
public:
    virtual void normalFunction() {
        std::cout << "Base: normalFunction" << std::endl;
    }

    virtual void constFunction() const {
        std::cout << "Base: constFunction" << std::endl;
    }

    virtual void finalFunction() final {
        std::cout << "Base: finalFunction" << std::endl;
    }

    virtual void constFinalFunction() const final {
        std::cout << "Base: constFinalFunction" << std::endl;
    }
};

class Derived : public Base {
public:
    void normalFunction() override {
        std::cout << "Derived: normalFunction" << std::endl;
    }

    void constFunction() const override {
        std::cout << "Derived: constFunction" << std::endl;
    }

    // Uncommenting the following would cause a compilation error:
    // void finalFunction() override {
    //     std::cout << "Derived: finalFunction" << std::endl;
    // }

    // Uncommenting the following would cause a compilation error:
    // void constFinalFunction() const override {
    //     std::cout << "Derived: constFinalFunction" << std::endl;
    // }
};

int main() {
    Base base;
    Derived derived;

    Base* ptr = &derived;

    ptr->normalFunction();    // Calls Derived::normalFunction
    ptr->constFunction();     // Calls Derived::constFunction
    ptr->finalFunction();     // Calls Base::finalFunction
    ptr->constFinalFunction();// Calls Base::constFinalFunction

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42m22ftys).

Now, let's break down the differences between `const` and `final` functions:

1. `const` Functions:
   * Purpose: To indicate that the function doesn't modify the object's state.
   * Syntax: Placed after the function declaration.
   * Effect on the object: Prevents modification of member variables (except those declared as `mutable`).
   * Inheritance: Can be overridden in derived classes (unless also declared as `final`).
   *   Usage:

       ```cpp
       void constFunction() const {
           // Implementation
       }
       ```
   * Key points:
     * Can only call other `const` member functions of the class.
     * Guarantees that the function won't modify the object's state.
     * Allows the function to be called on const objects.
     * Important for const correctness in C++ programming.
2. `final` Functions:
   * Purpose: To prevent further inheritance or overriding of the function.
   * Syntax: Placed after the function declaration (after `override` if present).
   * Effect on inheritance: Prevents the function from being overridden in derived classes.
   * Inheritance: Cannot be overridden in derived classes.
   *   Usage:

       ```cpp
       void finalFunction() final {
           // Implementation
       }
       ```
   * Key points:
     * Stops the virtual function call hierarchy at this point.
     * Useful for preventing further modifications to a function's behavior in a class hierarchy.
     * Can be combined with `virtual` and `override`.
3. Key Differences:
   * `const` is about the function's effect on the object's state, while `final` is about the function's inheritance behavior.
   * `const` functions can be overridden (unless also `final`), but `final` functions cannot be overridden at all.
   * `const` affects how the function can be used (on const objects) and what it can do (not modify non-mutable members), while `final` affects how the class can be inherited.
4.  Combining `const` and `final`: You can use both `const` and `final` on a function:

    ```cpp
    void constFinalFunction() const final {
        // Implementation
    }
    ```

    This creates a function that:

    * Doesn't modify the object's state (`const`)
    * Can't be overridden in derived classes (`final`)
5. Use Cases:
   * Use `const` for functions that don't modify the object's state, to enforce const correctness.
   * Use `final` when you want to prevent further overriding in a class hierarchy, often for security or design reasons.
6. Impact on Performance:
   * `const` functions can potentially allow for certain compiler optimizations.
   * `final` functions can sometimes be optimized by the compiler since it knows they won't be overridden.

Remember, `const` is about the contract of not modifying the object, while `final` is about the design of your class hierarchy. They serve different purposes and can be used independently or together depending on your needs.
