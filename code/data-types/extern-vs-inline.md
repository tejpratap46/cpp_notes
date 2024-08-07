# extern vs inline

Key differences between `extern` and `inline` variables in C++:

1. `extern` variables:
   * Declare a variable that is defined elsewhere (usually in another file)
   * Used to share global variables across multiple files
   * Do not allocate storage for the variable
   * Typically used in header files to declare variables defined in source files
2. `inline` variables (introduced in C++17):
   * Define a variable with external linkage that can be defined in multiple translation units
   * Ensure all definitions refer to the same object across the entire program
   * Allow header-only libraries to define global variables without violating the One Definition Rule
   * Implicitly have external linkage (unless explicitly declared `static`)

Here's a quick example to illustrate:

```cpp
// header.h
extern int globalVar; // Declaration of a variable defined elsewhere
inline int inlineVar = 10; // Definition of an inline variable

// source1.cpp
#include "header.h"
int globalVar = 5; // Definition of the extern variable

// source2.cpp
#include "header.h"
// Can use both globalVar and inlineVar here
```

In this example, `globalVar` is declared as `extern` in the header and defined in `source1.cpp`, while `inlineVar` is defined inline in the header and can be used in multiple source files.

The main advantages of `inline` variables are:

1. They can be defined in headers without causing multiple definition errors
2. They provide better encapsulation for header-only libraries
3. They can improve performance by allowing the compiler to optimize more aggressively

***

#### How to implement a singleton class using both extern and inline variables in C++. This comparison will highlight the differences and advantages of each approach.

```cpp
// Singleton.h

#ifndef SINGLETON_H
#define SINGLETON_H

#include <iostream>

// Extern approach
class SingletonExtern {
private:
    SingletonExtern() = default;
    SingletonExtern(const SingletonExtern&) = delete;
    SingletonExtern& operator=(const SingletonExtern&) = delete;

public:
    static SingletonExtern& getInstance();
    void someMethod() { std::cout << "SingletonExtern method called\n"; }
};

extern SingletonExtern& singletonExternInstance;

// Inline approach (C++17 and later)
class SingletonInline {
private:
    SingletonInline() = default;
    SingletonInline(const SingletonInline&) = delete;
    SingletonInline& operator=(const SingletonInline&) = delete;

public:
    static SingletonInline& getInstance() {
        static SingletonInline instance;
        return instance;
    }
    void someMethod() { std::cout << "SingletonInline method called\n"; }
};

#endif // SINGLETON_H

// Singleton.cpp

#include "Singleton.h"

// Extern approach implementation
SingletonExtern& SingletonExtern::getInstance() {
    static SingletonExtern instance;
    return instance;
}

SingletonExtern& singletonExternInstance = SingletonExtern::getInstance();

// Main.cpp

#include "Singleton.h"

int main() {
    // Using extern singleton
    singletonExternInstance.someMethod();
    SingletonExtern::getInstance().someMethod();

    // Using inline singleton
    SingletonInline::getInstance().someMethod();

    return 0;
}
```

Let me explain the key differences between these two approaches:

1. Extern Approach:
   * We declare an `extern` variable `singletonExternInstance` in the header file.
   * The actual instance is defined in a separate .cpp file.
   * This approach separates the declaration and definition, which can be useful for compilation speed in large projects.
   * It requires a separate compilation unit (the .cpp file) to define the instance.
2. Inline Approach:
   * The `getInstance()` method is defined inline in the class definition.
   * No separate .cpp file is needed for the implementation.
   * This approach is more concise and can be used in header-only libraries.
   * It's generally preferred in modern C++ (C++17 and later) for its simplicity and potential for better optimization.

Both approaches ensure that only one instance of the singleton is created. The inline approach is generally simpler to use and maintain, as it doesn't require a separate implementation file. However, the extern approach might be preferred in some cases, particularly in larger projects where you want to minimize header dependencies.
