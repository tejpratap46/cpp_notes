# 🪅 Data Types

* Integer types:
  * `char`: 1 byte
  * `short`: 2 bytes
  * `int`: 4 bytes (can be 2 bytes on some 16-bit systems)
  * `long`: 4 bytes on 32-bit systems, 8 bytes on 64-bit systems
  * `long long`: 8 bytes
* Unsigned integer types:
  * `unsigned char`: 1 byte
  * `unsigned short`: 2 bytes
  * `unsigned int`: 4 bytes
  * `unsigned long`: 4 bytes (32-bit) or 8 bytes (64-bit)
  * `unsigned long long`: 8 bytes
* Floating-point types:
  * `float`: 4 bytes
  * `double`: 8 bytes
  * `long double`: 12 or 16 bytes (compiler dependent)
* Boolean type:
  * `bool`: 1 byte
* Void type:
  * `void`: no size (used to indicate no value)
* Wide character type:
  * `wchar_t`: 2 or 4 bytes (compiler dependent)
* Character types (C++11 and later):
  * `char16_t`: 2 bytes
  * `char32_t`: 4 bytes
* Fixed-width integer types (C++11 and later):
  * `int8_t`, `uint8_t`: 1 byte
  * `int16_t`, `uint16_t`: 2 bytes
  * `int32_t`, `uint32_t`: 4 bytes
  * `int64_t`, `uint64_t`: 8 bytes

To get the exact size of a type on your specific system and compiler, you can use the `sizeof` operator:

```cpp
#include <iostream>

int main() {
    std::cout << "Size of int: " << sizeof(int) << " bytes\n";
    std::cout << "Size of long: " << sizeof(long) << " bytes\n";
    // Add more types as needed
    return 0;
}
```

Example showcasing overflow, causing wrap:

```cpp
#include <iostream>
#include <limits>

int main() {
    // Signed integer
    int signed_num = std::numeric_limits<int>::max(); // Maximum value
    signed_num++; // Increment by 1
    std::cout << "Signed num: " << signed_num << std::endl; // Output: negative limit

    // Unsigned integer
    unsigned int unsigned_num = std::numeric_limits<unsigned int>::max(); // Maximum value
    unsigned_num++; // Increment by 1
    std::cout << "Unsigned num: " << unsigned_num << std::endl; // Output: 0 (wraps around)

    return 0;
}

```

> Run it [here](https://onecompiler.com/cpp/42n8wmcpr).
