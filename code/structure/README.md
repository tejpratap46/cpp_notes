---
description: Collection of different data types
---

# 🏗️ Structure

*   Basic Definition: A struct is defined using the `struct` keyword, followed by the struct name and a block containing member variables.

    ```cpp
    struct Point {
        int x;
        int y;
    };
    ```
*   Creating Instances: You can create instances of a struct like this:

    ```cpp
    Point p1;
    p1.x = 10;
    p1.y = 20;

    // Or using an initializer list (C++11 and later)
    Point p2 = {30, 40};
    ```
*   Member Access: Access struct members using the dot (.) operator:

    ```cpp
    std::cout << "p1: (" << p1.x << ", " << p1.y << ")" << std::endl;
    ```
*   Functions in Structs: Structs can also contain functions (methods):

    ```cpp
    struct Rectangle {
        int width;
        int height;

        int area() {
            return width * height;
        }
    };
    ```
*   Constructors: You can define constructors for initialization:

    ```cpp
    struct Person {
        std::string name;
        int age;

        Person(std::string n, int a) : name(n), age(a) {}
    };

    Person alice("Alice", 30);
    ```
* Default Access Specifier: In a struct, members are public by default (unlike in classes where they're private by default).
*   Nested Structs: You can nest structs within other structs:

    ```cpp
    struct Address {
        std::string street;
        std::string city;
    };

    struct Employee {
        std::string name;
        Address workAddress;
    };
    ```
*   Pointers to Structs: You can create pointers to structs and access members using the arrow (->) operator:

    ```cpp
    Point* pPtr = &p1;
    std::cout << pPtr->x << ", " << pPtr->y << std::endl;
    ```
* Struct vs Class: The main difference is the default access specifier. Structs are often used for simple data structures, while classes are used for more complex objects with behaviors.
* Memory Alignment: Structs can have padding between members for memory alignment. You can use `#pragma pack` or `__attribute__((packed))` to control this.

Example:

```cpp
#include <iostream>
#include <string>

struct Date {
    int day;
    int month;
    int year;

    Date(int d, int m, int y) : day(d), month(m), year(y) {}

    void display() {
        std::cout << day << "/" << month << "/" << year << std::endl;
    }
};

struct Person {
    std::string name;
    Date birthDate;

    Person(std::string n, Date bd) : name(n), birthDate(bd) {}

    void introduce() {
        std::cout << "Hi, I'm " << name << ". I was born on ";
        birthDate.display();
    }
};

int main() {
    Date bobBirthDate(15, 6, 1990);
    Person bob("Bob", bobBirthDate);

    bob.introduce();

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzxu7me).
