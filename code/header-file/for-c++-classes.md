# For C++ Classes

1. Heade File:

```cpp
#ifndef PERSON_H
#define PERSON_H

#include <string>

class Person {
private:
    std::string name;
    int age;

public:
    Person(const std::string& name, int age);
    
    void setName(const std::string& name);
    std::string getName() const;
    
    void setAge(int age);
    int getAge() const;
    
    void introduce() const;
};

#endif // PERSON_H
```

2. Header Implementation:

```cpp
#include "Person.h"
#include <iostream>

Person::Person(const std::string& name, int age) : name(name), age(age) {}

void Person::setName(const std::string& name) {
    this->name = name;
}

std::string Person::getName() const {
    return name;
}

void Person::setAge(int age) {
    this->age = age;
}

int Person::getAge() const {
    return age;
}

void Person::introduce() const {
    std::cout << "Hello, my name is " << name << " and I'm " << age << " years old." << std::endl;
}
```

3. Main

```cpp
#include "Person.h"

int main() {
    Person alice("Alice", 30);
    alice.introduce();

    alice.setAge(31);
    alice.introduce();

    Person bob("Bob", 25);
    bob.introduce();

    return 0;
}
```
