# 'this' Pointer

The `this` pointer is a special pointer in C++ that points to the current instance of a class. It's an implicit parameter to all non-static member functions and has several important uses and characteristics.

```cpp
#include <iostream>
#include <string>

class Base {
protected:
    int value;

public:
    Base(int v) : value(v) {}

    // Using 'this' in operator overloading
    Base& operator+=(int x) {
        this->value += x;
        return *this;
    }

    // Virtual function using 'this'
    virtual void print() const {
        std::cout << "Base: " << this->value << std::endl;
    }

    // Using 'this' to call another member function
    void increment() {
        this->add(1);
    }

private:
    void add(int x) {
        value += x;
    }
};

class Derived : public Base {
private:
    std::string name;

public:
    Derived(int v, const std::string& n) : Base(v), name(n) {}

    // Using 'this' to access both base and derived members
    void print() const override {
        std::cout << "Derived: " << this->name << ", " << this->value << std::endl;
    }

    // Using 'this' to disambiguate between base and derived class methods
    void test() {
        this->Base::print();  // Call base class print
        this->print();        // Call derived class print
    }

    // Using 'this' in a template method
    template<typename T>
    void compareAndPrint(const T& other) const {
        if (this->value > other.value) {
            std::cout << this->name << " is greater" << std::endl;
        } else {
            std::cout << other.name << " is greater or equal" << std::endl;
        }
    }
};

int main() {
    Base b(10);
    b += 5;
    b.print();

    Derived d1(20, "Object1");
    Derived d2(30, "Object2");

    d1.test();

    d1 += 15;
    d1.print();

    d1.compareAndPrint(d2);

    // Using 'this' in polymorphism
    Base* ptr = &d1;
    ptr->print();  // Calls Derived::print()

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzwczg2).
