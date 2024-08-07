# 🔃 Operator overloading

Operator overloading in C++ allows you to define how operators behave when applied to objects of user-defined classes. This feature enables you to use standard operators like +, -, \*, /, =, etc., with your custom types, making your code more intuitive and readable.

Here's an example that demonstrates operator overloading:

```cpp
#include <iostream>

class Complex {
private:
    double real;
    double imag;

public:
    // Constructor
    Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}

    // Overload the + operator
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    // Overload the * operator
    Complex operator*(const Complex& other) const {
        return Complex(real * other.real - imag * other.imag,
                       real * other.imag + imag * other.real);
    }

    // Overload the == operator
    bool operator==(const Complex& other) const {
        return (real == other.real) && (imag == other.imag);
    }

    // Overload the << operator for easy output
    friend std::ostream& operator<<(std::ostream& os, const Complex& c) {
        os << c.real;
        if (c.imag >= 0) os << "+";
        os << c.imag << "i";
        return os;
    }
};

int main() {
    Complex a(1.0, 2.0);
    Complex b(3.0, 4.0);

    Complex sum = a + b;
    Complex product = a * b;

    std::cout << "a = " << a << std::endl;
    std::cout << "b = " << b << std::endl;
    std::cout << "a + b = " << sum << std::endl;
    std::cout << "a * b = " << product << std::endl;
    std::cout << "a == b: " << (a == b) << std::endl;

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42n8uketa).

In this example, we've created a `Complex` class to represent complex numbers and overloaded several operators:

1.  `+` operator: This allows us to add two Complex numbers.

    ```cpp
    Complex operator+(const Complex& other) const { ... }
    ```
2.  `*` operator: This enables multiplication of Complex numbers.

    ```cpp
    Complex operator*(const Complex& other) const { ... }
    ```
3.  `==` operator: This allows comparison of Complex numbers.

    ```cpp
    bool operator==(const Complex& other) const { ... }
    ```
4.  `<<` operator: This is overloaded as a friend function to allow easy output of Complex numbers.

    ```cpp
    friend std::ostream& operator<<(std::ostream& os, const Complex& c) { ... }
    ```

> Try it [here](https://onecompiler.com/cpp/42m76tgdr).

Key points about operator overloading:

1. You can overload most built-in operators in C++, but not all (e.g., `.`, `::`).
2. Operator overloading doesn't change the precedence or associativity of operators.
3. You can overload operators as member functions or as non-member functions.
4. Some operators (like =, \[], (), ->) must be overloaded as member functions.
5. The `friend` keyword is often used with operator overloading to give the operator function access to private members of the class.

When you run this program, it will output:

```
Copya = 1+2i
b = 3+4i
a + b = 4+6i
a * b = -5+10i
a == b: 0
```

This demonstrates how we can now use standard operators with our custom Complex class, making the code more intuitive and closer to mathematical notation.
