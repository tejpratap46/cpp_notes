# Custom vector, part 3

As we have seen in [custom-vector-part-2.md](custom-vector-part-2.md "mention"), using array operations, we are coping each element on by one and repeat once we are out of capacity.

We can directly operate on memory using `malloc`, `memcpy` and `realloc` operations.

Here is a example:

```cpp
#include <iostream>
#include <cstring>
#include <algorithm>

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

template<typename T>
class CustomVector {
private:
    T* data;
    size_t size;
    size_t capacity;

    void realloc(size_t newCapacity) {
        T* newData = static_cast<T*>(malloc(newCapacity * sizeof(T)));
        if (newData == nullptr) {
            throw std::bad_alloc();
        }
        
        if (data != nullptr) {
            memcpy(newData, data, size * sizeof(T));
            free(data);
        }
        
        data = newData;
        capacity = newCapacity;
    }

public:
    CustomVector() : data(nullptr), size(0), capacity(0) {}

    ~CustomVector() {
        clear();
        if (data != nullptr) {
            free(data);
        }
    }

    void push_back(const T& value) {
        if (size == capacity) {
            size_t newCapacity = (capacity == 0) ? 1 : capacity * 2;
            realloc(newCapacity);
        }
        memcpy(data + size, &value, sizeof(T));
        ++size;
    }

    void pop_back() {
        if (size > 0) {
            --size;
        }
    }

    T& operator[](size_t index) {
        if (index >= size) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }

    const T& operator[](size_t index) const {
        if (index >= size) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }

    size_t get_size() const {
        return size;
    }

    size_t get_capacity() const {
        return capacity;
    }

    void clear() {
        size = 0;
    }

    // Custom iterator implementation
    class Iterator {
    private:
        T* ptr;
    public:
        Iterator(T* p) : ptr(p) {}
        T& operator*() { return *ptr; }
        Iterator& operator++() { ++ptr; return *this; }
        bool operator!=(const Iterator& other) const { return ptr != other.ptr; }
    };

    Iterator begin() { return Iterator(data); }
    Iterator end() { return Iterator(data + size); }
};

// Example usage
int main() {
    CustomVector<MyInt> v;
    std::cout << "add fist" << std::endl;
    v.push_back(MyInt(35));
    
    for (size_t i = 0; i < v.get_size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    
    std::cout << "add second" << std::endl;
    v.push_back(MyInt(30));
    
    for (size_t i = 0; i < v.get_size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    
    std::cout << "add third" << std::endl;
    v.push_back(MyInt(25));

    for (size_t i = 0; i < v.get_size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    std::cout << "pop back" << std::endl;
    v.pop_back();

    for (size_t i = 0; i < v.get_size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    
    std::cout << "add fourth" << std::endl;
    v.push_back(MyInt(20));

    for (size_t i = 0; i < v.get_size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42ngh6ecv).

#### Output:

```
add fist
Constructor called for 35, address: 0x7fffffffd7d4
Deconstructor called for 35, address: 0x7fffffffd7d4
value: value: 35, address: 0x55555556b2c0
add second
Constructor called for 30, address: 0x7fffffffd7d4
Deconstructor called for 30, address: 0x7fffffffd7d4
value: value: 35, address: 0x55555556b2e0
value: value: 30, address: 0x55555556b2e4
add third
Constructor called for 25, address: 0x7fffffffd7d4
Deconstructor called for 25, address: 0x7fffffffd7d4
value: value: 35, address: 0x55555556b2c0
value: value: 30, address: 0x55555556b2c4
value: value: 25, address: 0x55555556b2c8
pop back
value: value: 35, address: 0x55555556b2c0
value: value: 30, address: 0x55555556b2c4
add fourth
Constructor called for 20, address: 0x7fffffffd7d4
Deconstructor called for 20, address: 0x7fffffffd7d4
value: value: 35, address: 0x55555556b2c0
value: value: 30, address: 0x55555556b2c4
value: value: 20, address: 0x55555556b2c8
```

Here, as compared to before, we have reduced number of memory operations.

But we still have a long way to go, unnecessary memory operations are still happening, we can stop them using something called as `emplace_back` provided by `std::vector`, which will allow us to handover class creating to `Vector` class itself, this reducing further more memory operations.
