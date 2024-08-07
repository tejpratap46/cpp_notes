# Other function declaration

1. Access Modifiers:

```cpp
class MyClass {
public:
    void publicFunc() { /* Accessible from anywhere */ }
protected:
    void protectedFunc() { /* Accessible within the class and derived classes */ }
private:
    void privateFunc() { /* Accessible only within the class */ }
};
```

2. Const Correctness

```cpp
class MyClass {
public:
    int getValue() const { return value_; } // Can be called on constant objects
    void setValue(int newValue) { value_ = newValue; } // Cannot be called on constant objects
private:
    int value_;
};
```

3. Virtual Functions

```cpp
class Base {
public:
    virtual void func() { std::cout << "Base::func()\n"; }
};

class Derived : public Base {
public:
    void func() override { std::cout << "Derived::func()\n"; }
};
```

4. Override and Final

```cpp
class Base {
public:
    virtual void func() = 0; // Pure virtual function
};

class Derived : public Base {
public:
    void func() override { /* Implementation */ }
};

class FinalClass : public Base {
public:
    void func() final override { /* Implementation */ } // Prevent further overriding
};
```

5. Static Functions

```cpp
class MyClass {
public:
    static int getCount() { return count_; }
    static void incrementCount() { count_++; }
private:
    static int count_;
};
```

6. Inline Functions

```cpp
inline int square(int x) { return x * x; }
```

7. Explicit Constructor

```cpp
class MyClass {
public:
    explicit MyClass(int value) : value_(value) {}
private:
    int value_;
};
```

8. Default Arguments

```cpp
void printMessage(std::string message, int count = 1) {
    for (int i = 0; i < count; ++i) {
        std::cout << message << std::endl;
    }
}
```

9. Function Overloading

```cpp
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
```

10. Function Templates

```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

// the call it using
int main() {
    int x = 10, y = 20;
    double a = 3.14, b = 2.718;
    std::string s1 = "hello", s2 = "world";

    std::cout << max(x, y) << std::endl; // Calls max<int>(x, y)
    std::cout << max(a, b) << std::endl; // Calls max<double>(a, b)
    std::cout << max(s1, s2) << std::endl; // Calls max<std::string>(s1, s2)
    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42kzznwt7).
