# Enum

An enum, short for enumeration, is a user-defined data type in C++ used to assign names to integral constants. Enums make the code more readable and maintainable by giving meaningful names to a set of related values.

There are two types of enums in C++:

1. Traditional C-style enums (introduced in C and carried over to C++)
2. Enum classes (introduced in C++11)

Let's look at both:

1. Traditional C-style enums:

```cpp
enum Color {
    RED,    // 0
    GREEN,  // 1
    BLUE    // 2
};

Color myColor = GREEN;
```

Key points:

* By default, the first enumerator is assigned the value 0, and each subsequent enumerator is incremented by 1.
*   You can assign specific values to enumerators:

    ```cpp
    enum Color {
        RED = 5,
        GREEN = 10,
        BLUE = 15
    };
    ```
* Enumerators are in the same scope as the enum, which can lead to name conflicts.
* They implicitly convert to integers.

2. Enum classes (C++11 and later):

```cpp
enum class Fruit : unsigned int {
    APPLE,
    BANANA,
    ORANGE
};

Fruit myFruit = Fruit::BANANA;
```

Key points:

* Enum classes provide stronger type safety.
* They don't implicitly convert to integers.
* Enumerators are scoped within the enum class.
* You can specify the underlying type (e.g., unsigned int).

Here's a more comprehensive example demonstrating both types:

```cpp
#include <iostream>

// Traditional enum
enum Color {
    RED,
    GREEN,
    BLUE
};

// Enum class
enum class Direction : char {
    NORTH = 'N',
    EAST = 'E',
    SOUTH = 'S',
    WEST = 'W'
};

int main() {
    // Using traditional enum
    Color paint = GREEN;
    int colorCode = paint;  // Implicit conversion to int
    std::cout << "Color code: " << colorCode << std::endl;

    // Using enum class
    Direction way = Direction::EAST;
    // std::cout << way; // This would not compile
    std::cout << "Direction: " << static_cast<char>(way) << std::endl;

    // Comparison
    if (paint == GREEN) {
        std::cout << "The paint is green." << std::endl;
    }

    if (way == Direction::EAST) {
        std::cout << "We're heading east." << std::endl;
    }

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42m76q3rd).

Benefits of using enums:

1. Improved code readability
2. Type safety (especially with enum classes)
3. Easy to maintain and modify related constants

Enum classes are generally preferred in modern C++ due to their stronger type safety and scoping rules. However, traditional enums are still widely used, especially in code bases that need to maintain compatibility with C or older C++ standards.
