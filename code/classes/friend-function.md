# Friend Function

Friend functions in C++ are a special type of functions that are granted access to private and protected members of a class, even though they are not members of that class.

Key points about friend functions:

1. Declaration: Friend functions are declared inside the class definition using the `friend` keyword, but they are not member functions of the class.
2. Access: They can access private and protected members of the class without being a member of that class.
3. Scope: They are not in the scope of the class, and they don't have a `this` pointer.
4. Declaration vs. Definition: The function can be declared as a friend in the class definition, but the actual function definition is outside the class.
5. Cannot be inherited: Friendship is not inherited, meaning if a base class has a friend function, it doesn't automatically become a friend of the derived class.

Here's a simple example to illustrate friend functions:

```cpp
#include <iostream>

class Box {
private:
    int width, height, depth;

public:
    Box(int w, int h, int d) : width(w), height(h), depth(d) {}

    // Declaration of friend function
    friend int getBoxVolume(const Box& b);

    // Friend function can be a member of another class
    friend class BoxPrinter;
};

// Definition of friend function
int getBoxVolume(const Box& b) {
    // Can access private members of Box
    return b.width * b.height * b.depth;
}

class BoxPrinter {
public:
    void printBoxDimensions(const Box& b) {
        // Can access private members of Box
        std::cout << "Width: " << b.width 
                  << ", Height: " << b.height 
                  << ", Depth: " << b.depth << std::endl;
    }
};

int main() {
    Box myBox(3, 4, 5);
    std::cout << "Volume: " << getBoxVolume(myBox) << std::endl;

    BoxPrinter printer;
    printer.printBoxDimensions(myBox);

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42m3t6sty).

In this example:

1. `getBoxVolume` is a friend function of the `Box` class. It can access private members of `Box`.
2. `BoxPrinter` is a friend class of `Box`. All its member functions can access private members of `Box`.
3. The `getBoxVolume` function and `BoxPrinter::printBoxDimensions` method can access `width`, `height`, and `depth` directly, even though they're private.

Use cases for friend functions:

1. When you need a function to have access to private members of a class, but you don't want it to be a member function.
2. For operator overloading, especially when the left-hand operand is not an object of the class (like stream insertion operators).
3. To allow a function to work intimately with two different classes.
