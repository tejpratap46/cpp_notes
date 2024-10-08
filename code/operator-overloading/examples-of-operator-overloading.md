# Examples of operator overloading

#### Arithmetic Operators

```cpp
#include <iostream>

class Complex {
public:
    double real, imag;
    Complex(double r, double i) : real(r), imag(i) {}

    // Overloading + operator
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
};

int main() {
    Complex c1(2, 3), c2(4, 5);
    Complex c3 = c1 + c2; // Using overloaded +
    std::cout << c3.real << " + " << c3.imag << "i" << std::endl;
    return 0;
}
```

#### Assignment Operators

```cpp
#include <iostream>
#include <cstring>

class StringWrapper {
private:
    char* str;

public:
    // Constructor
    StringWrapper(const char* s = nullptr) {
        if (s) {
            str = new char[strlen(s) + 1];
            strcpy(str, s);
        } else {
            str = new char[1];
            str[0] = '\0';
        }
    }

    // Destructor
    ~StringWrapper() {
        delete[] str;
    }

    // Copy constructor
    StringWrapper(const StringWrapper& other) {
        str = new char[strlen(other.str) + 1];
        strcpy(str, other.str);
    }

    // Assignment operator overloading
    StringWrapper& operator=(const StringWrapper& other) {
        if (this != &other) {  // Self-assignment check
            // Free the existing resource
            delete[] str;

            // Allocate new resource and copy
            str = new char[strlen(other.str) + 1];
            strcpy(str, other.str);
        }
        return *this;
    }

    // Method to get the string
    const char* getString() const {
        return str;
    }
};

int main() {
    StringWrapper s1("Hello");
    StringWrapper s2("World");
    StringWrapper s3 = s1;  // Copy constructor

    std::cout << "s1: " << s1.getString() << std::endl;
    std::cout << "s2: " << s2.getString() << std::endl;
    std::cout << "s3: " << s3.getString() << std::endl;

    s2 = s1;  // Assignment operator

    std::cout << "After s2 = s1:" << std::endl;
    std::cout << "s1: " << s1.getString() << std::endl;
    std::cout << "s2: " << s2.getString() << std::endl;

    return 0;
}
```

#### Comparison Operators

```cpp
#include <iostream>

class Person {
public:
    int age;
    Person(int a) : age(a) {}

    // Overloading < operator
    bool operator<(const Person& other) const {
        return age < other.age;
    }
};

int main() {
    Person p1(25), p2(30);
    if (p1 < p2) {
        std::cout << "p1 is younger than p2" << std::endl;
    }
    return 0;
}
```

#### Increment/Decrement Operators

```cpp
#include <iostream>

class Counter {
public:
    int count;
    Counter(int c) : count(c) {}

    // Overloading ++ operator
    Counter& operator++() {
        ++count;
        return *this;
    }
};

int main() {
    Counter c(5);
    ++c; // Using overloaded ++
    std::cout << c.count << std::endl;
    return 0;
}
```

#### Logical Operators

```cpp
// Overloading logical operators is less common and requires careful consideration.
// It's often better to use member functions for custom logic instead.
```

#### Bitwise Operators

```cpp
// Overloading bitwise operators is generally not recommended for custom classes.
#include <iostream>

class MyInt {
public:
    int value;

    MyInt(int val) : value(val) {}

    // Overloading the & operator
    MyInt operator&(const MyInt& other) const {
        // Custom logic for bitwise AND
        return MyInt(value & other.value);
    }
};

int main() {
    MyInt a(5), b(3);
    MyInt c = a & b; // Using the overloaded & operator
    std::cout << c.value << std::endl; // Output: 1
    return 0;
}
```

#### Member Access Operators

```cpp
#include <iostream>
#include <string>

// A simple class to be wrapped
class Person {
public:
    std::string name;
    int age;

    void introduce() {
        std::cout << "Hi, I'm " << name << " and I'm " << age << " years old." << std::endl;
    }
};

// Our wrapper class
class PersonWrapper {
private:
    Person* ptr;

public:
    PersonWrapper(Person* p) : ptr(p) {}

    // Overloaded member access operator
    Person* operator->() {
        std::cout << "Accessing member of Person object" << std::endl;
        return ptr;
    }
};

int main() {
    Person p{"Alice", 30};
    PersonWrapper wrapped(&p);

    // Using the wrapper to access Person members
    wrapped->name = "Bob";
    wrapped->age = 25;
    wrapped->introduce();

    return 0;
}
```

#### Subscript Operator

```cpp
#include <iostream>

class MyArray {
public:
    int arr[10];

    // Overloading [] operator
    int& operator[](int index) {
        return arr[index];
    }
};

int main() {
    MyArray myArray;
    myArray[3] = 5; // Using overloaded []
    std::cout << myArray[3] << std::endl;
    return 0;
}
```

#### Function Call Operator

```cpp
#include <iostream>

class Callable {
public:
    void operator()(int x) {
        std::cout << "Called with: " << x << std::endl;
    }
};

int main() {
    Callable obj;
    obj(10); // Using overloaded ()
    return 0;
}
```

#### Comma Operator

```cpp
class MyClass {
public:
    int value;

    MyClass(int v) : value(v) {}

    MyClass& operator,(const MyClass& other) {
        // Custom logic here
        value += other.value;
        return *this;
    }
};

int main() {
    MyClass obj1(5), obj2(3);
    obj1, obj2; // Overloaded comma operator
    std::cout << obj1.value << std::endl; // Output: 8
    return 0;
}
```

#### New and Delete Operators

```cpp
#include <iostream>

class MyClass {
public:
    int data;

    // Overloaded new operator
    void* operator new(size_t size) {
        std::cout << "Overloaded new operator called\n";
        // You can customize memory allocation here
        void* ptr = malloc(size);
        return ptr;
    }

    // Overloaded delete operator
    void operator delete(void* ptr) {
        std::cout << "Overloaded delete operator called\n";
        // You can perform custom deallocation here
        free(ptr);
    }
};

int main() {
    MyClass* obj = new MyClass();
    delete obj;
    return 0;
}
```
