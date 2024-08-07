---
description: >-
  These directives allow you to include or exclude code based on certain
  conditions
---

# #ifdef

If we include a header file 2 times (maybe in multiple files), we will get error saying multiple declaration found.

To overcome this, we need to ignore multiple inclusion, we define a [macro](define.md). which we check if `ifdef` and ignore inclusion if already incuded.

Here is an example:

```cpp
#define DEBUG

#ifdef DEBUG
    std::cout << "Debug mode is on" << std::endl;
#endif

#ifndef NDEBUG
    // Code for debug builds
#else
    // Code for release builds
#endif
```

Or another example, we check system config, if system is `unix` we use `cls` and if it us `linux` we use `clear` and many more.

```cpp
#ifdef _WIN32
    #define CLEAR_SCREEN "cls"
#else
    #define CLEAR_SCREEN "clear"
#endif

#if defined(__cplusplus) && __cplusplus >= 201703L
    // Use C++17 features
#elif defined(__cplusplus) && __cplusplus >= 201402L
    // Use C++14 features
#else
    #error "This program requires at least C++14"
#endif
```
