# Virtual functions

Inherit methods and member of parent classes.

Virtual functions in C++ are a key feature of object-oriented programming that enable polymorphism. Here's a concise explanation:

1. Definition: A virtual function is a member function declared in a base class and redefined in derived classes.
2. Purpose: They allow a program to call methods of a derived class through a pointer or reference of the base class type.
3. Declaration: Declared using the 'virtual' keyword in the base class.
4. Late binding: The function call is resolved at runtime, not compile-time.
5. Pure virtual functions: Defined with "= 0" and make the class abstract.
6. Virtual destructors: Often used to ensure proper cleanup of derived objects.
7. Virtual table (vtable): C++ uses this behind the scenes for implementation.

```cpp
#include <iostream>

class Animal {
public:
    virtual void makeSound() {
        std::cout << "The animal makes a sound" << std::endl;
    }
    
    virtual ~Animal() {
        std::cout << "Animal destructor called" << std::endl;
    }
};

class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "The dog barks: Woof!" << std::endl;
    }
    
    ~Dog() override {
        std::cout << "Dog destructor called" << std::endl;
    }
};

class Cat : public Animal {
public:
    void makeSound() override {
        std::cout << "The cat meows: Meow!" << std::endl;
    }
    
    ~Cat() override {
        std::cout << "Cat destructor called" << std::endl;
    }
};

int main() {
    Animal* animal1 = new Dog();
    Animal* animal2 = new Cat();
    
    animal1->makeSound();  // Outputs: The dog barks: Woof!
    animal2->makeSound();  // Outputs: The cat meows: Meow!
    
    delete animal1;  // Calls Dog destructor, then Animal destructor
    delete animal2;  // Calls Cat destructor, then Animal destructor
    
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzzezgv).
