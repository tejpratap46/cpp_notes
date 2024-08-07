# Custom vector, part 2

Now, we have created a vector class that will add any new element and resize to any limit (at least till your app goes out of memory).

Now, lets try it with a class object, which will store elements on heap, here we can track added items constructor/deconstructor calls.

Here, we have created a wrapper class on `int`, where it will keep hold for a integer value.

We have overridden multiple constructors and deconstructors, we log these events to understand more of what happens internally.

```cpp
#include <iostream>

class MyInt {
private:
    int _int;

public:
    MyInt() : _int(0) {
        std::cout << "Default Constructor called for " << _int << ", address: " << &_int << std::endl;
    }

    MyInt(int a) : _int(a) {
        std::cout << "Constructor called for " << _int << ", address: " << &_int << std::endl;
    }

    ~MyInt() {
        std::cout << "Deconstructor called for " << _int << ", address: " << &_int << std::endl;
    }

    // Copy constructor
    MyInt(const MyInt& other): _int(other._int) {
        std::cout << "Copy constructor called for " << _int << ", address: " << &_int << std::endl;
    }

    // Move constructor
    MyInt(MyInt&& other) noexcept : _int(other._int) {
        std::cout << "Move constructor called for " << _int << ", address: " << &_int << std::endl;
    }

    void introduce() const {
        std::cout << "MyInt Value:  " << _int << ", address: " << &_int << std::endl;
    }

    MyInt& operator=(const MyInt& other) {
        if (this != &other) {
            _int = other._int;
        }
        return *this;
    }

    friend std::ostream& operator<<(std::ostream& os, const MyInt& obj);
};

std::ostream& operator<<(std::ostream& os, const MyInt& obj) {
    os << "value: " << obj._int;
    return os;
}

template <typename T>
class MyVector {
public:
    MyVector() : _data(nullptr), _size(0), capacity(0) {}

    ~MyVector() {
        delete[] _data;
    }

    void push_back(const T& value) {
        if (_size == capacity) {
            resize();
        }
        _data[_size++] = value;
    }

    void pop_back() {
        if (_size > 0) {
            --_size;
        }
    }

    T& operator[](size_t index) {
        return _data[index];
    }

    const T& operator[](size_t index) const {
        return _data[index];
    }

    size_t size() const {
        return _size;
    }

private:
    T* _data;
    size_t _size;
    size_t capacity;

    void resize() {
        capacity = capacity == 0 ? 1 : capacity * 2;
        T* new_data = new T[capacity];
        for (size_t i = 0; i < _size; ++i) {
            new_data[i] = _data[i];
        }
        delete[] _data;
        _data = new_data;
    }
};

int main() {
    MyVector<MyInt> v;
    std::cout << "add fist" << std::endl;
    v.push_back(MyInt(35));
    
    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    
    std::cout << "add second" << std::endl;
    v.push_back(MyInt(30));
    
    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    
    std::cout << "add third" << std::endl;
    v.push_back(MyInt(25));

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    std::cout << "pop back" << std::endl;
    v.pop_back();

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    
    std::cout << "add fourth" << std::endl;
    v.push_back(MyInt(20));

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    return 0;
}
```

#### Output:

```
add fist
Constructor called for 35, address: 0x7ffd588620c4
Default Constructor called for 0, address: 0x560e071ddec8
Deconstructor called for 35, address: 0x7ffd588620c4
value: value: 35, address: 0x560e071ddec8
add second
Constructor called for 30, address: 0x7ffd588620c4
Default Constructor called for 0, address: 0x560e071ddee8
Default Constructor called for 0, address: 0x560e071ddeec
Deconstructor called for 35, address: 0x560e071ddec8
Deconstructor called for 30, address: 0x7ffd588620c4
value: value: 35, address: 0x560e071ddee8
value: value: 30, address: 0x560e071ddeec
add third
Constructor called for 25, address: 0x7ffd588620c4
Default Constructor called for 0, address: 0x560e071ddec8
Default Constructor called for 0, address: 0x560e071ddecc
Default Constructor called for 0, address: 0x560e071dded0
Default Constructor called for 0, address: 0x560e071dded4
Deconstructor called for 30, address: 0x560e071ddeec
Deconstructor called for 35, address: 0x560e071ddee8
Deconstructor called for 25, address: 0x7ffd588620c4
value: value: 35, address: 0x560e071ddec8
value: value: 30, address: 0x560e071ddecc
value: value: 25, address: 0x560e071dded0
pop back
value: value: 35, address: 0x560e071ddec8
value: value: 30, address: 0x560e071ddecc
add fourth
Constructor called for 20, address: 0x7ffd588620c4
Deconstructor called for 20, address: 0x7ffd588620c4
value: value: 35, address: 0x560e071ddec8
value: value: 30, address: 0x560e071ddecc
value: value: 20, address: 0x560e071dded0
Deconstructor called for 0, address: 0x560e071dded4
Deconstructor called for 20, address: 0x560e071dded0
Deconstructor called for 30, address: 0x560e071ddecc
Deconstructor called for 35, address: 0x560e071ddec8
```

Here, lets look at the output:

As we look at the logs,&#x20;

1. We create a new object using Parameterised Constructor.
2. Then we check if `size == capacity`, here it comes yes.
3. Now we create an array of size 1, filled with default object.
4. After creating new array, we call default constructor to create a new object to fill it initially.
5. Then, we copy all elements from previous array to new array with increased size.
6. After copying old array, now we can delete it from memory as all elements are safe in new array.
7. Repeat `2` to `6` till we have added all elements.

As we see, we do a lot of memory operations for storing new data into vector.

Here are steps for each cycle:

1. Create multiple objects.
2. Copy them to new memory location.
3. Delete old data.

This consume precious memory and CPU cycle for simple operations, in next lesson, we will see how we can optimise this.
