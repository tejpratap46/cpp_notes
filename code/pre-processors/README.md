---
description: 'Those #Tag inside our program'
---

# ⏮️ Pre-Processors

Preprocessors in C++ are directives that are processed before the actual compilation of your code begins. They allow you to perform certain operations on your source code before it's compiled. Here's a concise overview of preprocessors in C++:

1.  Inclusion of header files:

    ```cpp
    #include <iostream>  // For standard library headers
    #include "myheader.h"  // For your own headers
    ```
2.  Macro definitions:

    ```cpp
    #define PI 3.14159
    #define SQUARE(x) ((x) * (x))
    ```
3.  Conditional compilation:

    ```cpp
    #ifdef DEBUG
      // Debug code
    #endif
    ```
4.  File inclusion guards:

    ```cpp
    #ifndef MYHEADER_H
    #define MYHEADER_H
    // Header content
    #endif
    ```
5.  Pragma directives:

    ```cpp
    #pragma once
    ```

These directives help with code organization, portability, and can sometimes improve performance.
