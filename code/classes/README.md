# 🏢 Classes

Classes are a fundamental concept in C++, providing a way to create user-defined types that encapsulate data and functions. They are a key feature of object-oriented programming in C++.

1.  Basic Structure:

    ```cpp
    class ClassName {
    public:
        // Public members
    private:
        // Private members
    protected:
        // Protected members
    };
    ```
2. Access Specifiers:
   * `public`: Accessible from outside the class
   * `private`: Accessible only within the class (default for classes)
   * `protected`: Accessible within the class and derived classes
3. Data Members: Variables declared within the class.
4. Member Functions: Functions declared within the class that operate on the class data.
5. Constructors: Special member functions for initializing objects.
6. Destructors: Special member functions for cleaning up when an object is destroyed.
7. This Pointer: Implicit pointer to the current object instance.
8. Static Members: Members shared by all instances of the class.
9. Const Members: Members that can't modify the object's state.
10. Friend Functions: Non-member functions given access to private members.

Example:

```cpp
#include <iostream>
#include <string>

class Person {
private:
    std::string name;
    int age;
    static int count;  // Static member

public:
    // Constructor
    Person(const std::string& n, int a) : name(n), age(a) {
        count++;
    }

    // Destructor
    ~Person() {
        count--;
    }

    // Member function
    void introduce() const {
        std::cout << "Hi, I'm " << name << " and I'm " << age << " years old." << std::endl;
    }

    // Static member function
    static int getCount() {
        return count;
    }

    // Getter (const member function)
    std::string getName() const {
        return name;
    }

    // Setter
    void setAge(int a) {
        age = a;
    }

    // Friend function declaration
    friend void displayAge(const Person& p);
};

// Static member initialization
int Person::count = 0;

// Friend function definition
void displayAge(const Person& p) {
    std::cout << p.name << " is " << p.age << " years old." << std::endl;
}

int main() {
    Person alice("Alice", 30);
    Person bob("Bob", 25);

    alice.introduce();
    bob.introduce();

    std::cout << "Total persons: " << Person::getCount() << std::endl;

    displayAge(alice);  // Friend function call

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzzch9q).
