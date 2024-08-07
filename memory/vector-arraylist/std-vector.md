# std::vector

Here's a brief explanation along with an example:

```cpp
#include <iostream>
#include <vector>
#include <string>

class Person {
private:
    std::string name;
    int age;

public:
    Person(const std::string& n, int a) : name(n), age(a) {
        std::cout << "Constructor called for " << name << std::endl;
    }

    // Copy constructor
    Person(const Person& other) : name(other.name), age(other.age) {
        std::cout << "Copy constructor called for " << name << std::endl;
    }

    // Move constructor
    Person(Person&& other) noexcept : name(std::move(other.name)), age(other.age) {
        std::cout << "Move constructor called for " << name << std::endl;
    }

    void introduce() const {
        std::cout << "Hi, I'm " << name << " and I'm " << age << " years old." << std::endl;
    }
};

int main() {
    std::cout << "Creating initial vector:" << std::endl;
    std::vector<Person> people;
    
    std::cout << "\nAdding people to vector:" << std::endl;
    people.push_back(Person("Jhon", 35));
    people.emplace_back("Alice", 30);
    people.emplace_back("Bob", 25);
    
    std::cout << "\nVector size: " << people.size() << std::endl;
    
    std::cout << "\nCreating a copy of the vector:" << std::endl;
    std::vector<Person> people_copy = people;
    
    std::cout << "\nIntroducing people from original vector:" << std::endl;
    for (const auto& person : people) {
        person.introduce();
    }
    
    std::cout << "\nIntroducing people from copied vector:" << std::endl;
    for (const auto& person : people_copy) {
        person.introduce();
    }
    
    std::cout << "\nAdding a new person to original vector:" << std::endl;
    people.emplace_back("Charlie", 35);
    
    std::cout << "\nOriginal vector size: " << people.size() << std::endl;
    std::cout << "Copied vector size: " << people_copy.size() << std::endl;

    return 0;
}
```

Let's break down the key points:

1. We define a `Person` class with a name and age.
2. The class includes a regular constructor, a copy constructor, and a move constructor. Each constructor logs when it's called.
3. In the `main` function, we create a vector of `Person` objects.
4. We use `emplace_back()` to construct `Person` objects directly in the vector, which is more efficient than `push_back()` for non-trivial objects.
5. We create a copy of the vector, which triggers the copy constructor for each `Person` object.
6. We demonstrate that the original and copied vectors are independent by adding a new person to the original vector.

When you run this program, you'll see logs for each constructor call, allowing you to track when objects are being created, copied, or moved. This is particularly useful for understanding the behavior of vectors and optimizing performance.

Key observations from the output:

1. When adding elements with `emplace_back()`, only the regular constructor is called.
2. When creating a copy of the vector, the copy constructor is called for each element.
3. The original and copied vectors are independent; changes to one don't affect the other.

This example showcases how vectors work with custom classes and highlights the importance of properly implementing constructors, especially when dealing with resource management in more complex classes.
