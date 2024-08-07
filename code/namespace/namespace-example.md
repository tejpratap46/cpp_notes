# Namespace Example

Here is an `GameEngine` example:

```cpp
#include <iostream>
#include <string>

// Namespace for a graphics library
namespace GraphicsLib {
    struct Color {
        int r, g, b;
    };

    void draw(const std::string& shape, const Color& color) {
        std::cout << "GraphicsLib: Drawing a " << shape << " with color RGB("
                  << color.r << "," << color.g << "," << color.b << ")" << std::endl;
    }

    int getArea(int width, int height) {
        std::cout << "GraphicsLib: Calculating area of a rectangle" << std::endl;
        return width * height;
    }
}

// Namespace for a math library
namespace MathLib {
    struct Point {
        double x, y;
    };

    void draw(const Point& start, const Point& end) {
        std::cout << "MathLib: Drawing a line from (" << start.x << "," << start.y
                  << ") to (" << end.x << "," << end.y << ")" << std::endl;
    }

    double getArea(double radius) {
        std::cout << "MathLib: Calculating area of a circle" << std::endl;
        return 3.14159 * radius * radius;
    }
}

// A function in the global namespace
void draw() {
    std::cout << "Global: Drawing nothing in particular" << std::endl;
}

int main() {
    // Using fully qualified names
    GraphicsLib::Color red = {255, 0, 0};
    GraphicsLib::draw("square", red);

    MathLib::Point p1 = {0, 0}, p2 = {5, 5};
    MathLib::draw(p1, p2);

    // Calling the global draw function
    ::draw();

    // Using namespace directives (generally avoided in practice)
    using namespace GraphicsLib;
    using namespace MathLib;

    // This would cause an error due to ambiguity:
    // draw(/* parameters */);

    // Resolving the ambiguity
    GraphicsLib::draw("circle", {0, 255, 0});
    MathLib::draw({1, 1}, {4, 5});

    // Functions with the same name but different parameters
    std::cout << "Rectangle area: " << GraphicsLib::getArea(4, 5) << std::endl;
    std::cout << "Circle area: " << MathLib::getArea(3) << std::endl;

    // Using a namespace alias
    namespace GL = GraphicsLib;
    GL::Color blue = {0, 0, 255};
    GL::draw("triangle", blue);

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzyhmwc).

This example demonstrates several important concepts related to namespace conflict resolution:

1. Same Function Names in Different Namespaces: Both `GraphicsLib` and `MathLib` have functions named `draw` and `getArea`, but with different parameters and implementations.
2.  Fully Qualified Names: We use fully qualified names to explicitly specify which namespace's function we want to call:

    ```cpp
    cppCopyGraphicsLib::draw("square", red);
    MathLib::draw(p1, p2);
    ```
3.  Global Namespace: We define a `draw` function in the global namespace and call it using the global namespace operator `::`:

    ```cpp
    cppCopy::draw();
    ```
4.  Using Directives and Ambiguity: We demonstrate how using directives can lead to ambiguity:

    ```cpp
    cppCopyusing namespace GraphicsLib;
    using namespace MathLib;
    // draw(/* parameters */); // This would cause a compilation error
    ```
5.  Resolving Ambiguity: Even after using directives, we can still use fully qualified names to resolve ambiguity:

    ```cpp
    cppCopyGraphicsLib::draw("circle", {0, 255, 0});
    MathLib::draw({1, 1}, {4, 5});
    ```
6.  Overloading Across Namespaces: The `getArea` function has different parameters in each namespace, demonstrating how function overloading works across namespaces:

    ```cpp
    cppCopyGraphicsLib::getArea(4, 5)
    MathLib::getArea(3)
    ```
7.  Namespace Alias: We use a namespace alias to create a shorter name for `GraphicsLib`:

    ```cpp
    cppCopynamespace GL = GraphicsLib;
    GL::draw("triangle", blue);
    ```

Key points about namespace conflict resolution:

1. Namespaces allow you to use the same function names in different contexts without conflicts.
2. Fully qualified names always provide unambiguous access to namespace members.
3. Using directives (`using namespace`) can lead to naming conflicts and should be used cautiously, especially in header files.
4. Function overloading works across namespaces, allowing functions with the same name but different parameters.
5. Namespace aliases can provide shorter names for long namespace names, improving code readability.
