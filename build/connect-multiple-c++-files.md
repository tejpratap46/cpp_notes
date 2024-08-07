---
description: 'Here is how to connect multiple c++ file:'
---

# 🔧 Connect multiple C++ Files

{% file src="../.gitbook/assets/linker_example.zip" %}
Sample Code for linker using g++
{% endfile %}

#### Here is a code example using multiple files:

<pre class="language-cpp"><code class="lang-cpp"><strong>// File: math_operations.h
</strong>#ifndef MATH_OPERATIONS_H
#define MATH_OPERATIONS_H

// Function declarations
int add(int a, int b);
int subtract(int a, int b);

// Variable declaration with external linkage
extern int globalValue;

#endif // MATH_OPERATIONS_H
</code></pre>

<pre class="language-cpp"><code class="lang-cpp"><strong>// File: math_operations.cpp
</strong>#include "math_operations.h"

// Function definitions
int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

// Variable definition
int globalValue = 10;
</code></pre>

<pre class="language-cpp"><code class="lang-cpp"><strong>// File: main.cpp
</strong>#include &#x3C;iostream>
#include "math_operations.h"

int main() {
    std::cout &#x3C;&#x3C; "Sum: " &#x3C;&#x3C; add(5, 3) &#x3C;&#x3C; std::endl;
    std::cout &#x3C;&#x3C; "Difference: " &#x3C;&#x3C; subtract(10, 4) &#x3C;&#x3C; std::endl;
    std::cout &#x3C;&#x3C; "Global value: " &#x3C;&#x3C; globalValue &#x3C;&#x3C; std::endl;
    return 0;
}
</code></pre>

***

Now, let's break down how these files are linked:

1. Header files and source files:
   * `math_operations.h` is a header file containing function declarations and an external variable declaration.
   * `math_operations.cpp` is a source file with the implementations of the functions declared in the header.
   * `main.cpp` is the main source file that uses the functions defined in `math_operations`.
2. \#include directive:
   * `math_operations.cpp` includes `math_operations.h` to ensure the function implementations match the declarations.
   * `main.cpp` includes `math_operations.h` to access the function declarations and the external variable.
3. External linkage:
   * `globalValue` is declared with `extern` in the header, making it accessible across multiple files.
   * It's defined in `math_operations.cpp` and can be used in `main.cpp`.
4. Function declarations and definitions:
   * Functions are declared in `math_operations.h` and defined in `math_operations.cpp`.
   * This allows `main.cpp` to use these functions by including only the header file.

To compile and link these files, you would use a command like:

<pre class="language-sh"><code class="lang-sh"><strong>g++ main.cpp math_operations.cpp -o program
</strong></code></pre>

This compiles both source files and links them together into an executable named "program".

The `#ifndef`, `#define`, and `#endif` in the header file create an "include guard" to prevent multiple inclusions of the same header, which can cause compilation errors.
