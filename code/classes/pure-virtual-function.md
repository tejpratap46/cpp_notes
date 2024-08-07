---
description: Interface/abstract classes in c++
---

# Pure virtual function

Pure virtual functions are used to create abstract base classes, which cannot be instantiated and must be inherited from.

```cpp
#include <iostream>

// Abstract base class
class Shape {
public:
    // Pure virtual function
    virtual double area() const = 0;
    
    // Regular virtual function
    virtual void display() const {
        std::cout << "This is a shape." << std::endl;
    }
    
    virtual ~Shape() {
        std::cout << "Shape destructor called" << std::endl;
    }
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}

    // Implementation of the pure virtual function
    double area() const override {
        return 3.14159 * radius * radius;
    }

    void display() const override {
        std::cout << "This is a circle with radius " << radius << std::endl;
    }

    ~Circle() override {
        std::cout << "Circle destructor called" << std::endl;
    }
};

class Rectangle : public Shape {
private:
    double width;
    double height;

public:
    Rectangle(double w, double h) : width(w), height(h) {}

    // Implementation of the pure virtual function
    double area() const override {
        return width * height;
    }

    void display() const override {
        std::cout << "This is a rectangle with width " << width << " and height " << height << std::endl;
    }

    ~Rectangle() override {
        std::cout << "Rectangle destructor called" << std::endl;
    }
};

int main() {
    // Shape shape;  // This would cause a compile error

    Shape* circle = new Circle(5);
    Shape* rectangle = new Rectangle(4, 6);

    std::cout << "Circle area: " << circle->area() << std::endl;
    circle->display();

    std::cout << "Rectangle area: " << rectangle->area() << std::endl;
    rectangle->display();

    delete circle;
    delete rectangle;

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzzhdtg).
