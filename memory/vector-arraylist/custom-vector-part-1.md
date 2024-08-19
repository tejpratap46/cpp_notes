# Custom vector, part 1

As explained before, what us vector and how it works. In this lesson, we will  try to create vector implementation by ourself, let's begin.

Here is the algorithm:

1. Create a generic class with `template`, it has 3 things:
   1. `data` to store data pointer.
   2. `size` to store current size of vector.
   3. `capacity` to keep track of capacity of vector, vector will be reallocated once this capacity is reached by current `size` of vector.
2. A method `push_back` to add new elements to vector.
3. If `size == capacity`, then copy all current data to a different array with increased capacity.
4. Else add  new data at the end of current vector.
5. Repeat `2` to `4` on every push.

```cpp
#include <iostream>

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
            // delete &_data[i];
        }
        delete[] _data;
        _data = new_data;
    }
};

int main() {
    MyVector<int> v;
    std::cout << "add fist" << std::endl;
    v.push_back(35);

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    std::cout << "add second" << std::endl;
    v.push_back(30);

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    std::cout << "add third" << std::endl;
    v.push_back(25);

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    std::cout << "Pop Back" << std::endl;

    v.pop_back();

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }

    std::cout << "add Fourth" << std::endl;
    v.push_back(20);

    for (size_t i = 0; i < v.size(); ++i) {
        std::cout << "value: " << v[i] << ", address: " << &v[i] << std::endl;
    }
    std::cout << std::endl;

    return 0;
}
```

> Run it [here](https://onecompiler.com/cpp/42ng6ddpa).

#### Output:

```
add fist
value: 35, address: 0x55dcb2e3eec0
add second
value: 35, address: 0x55dcb2e3eee0
value: 30, address: 0x55dcb2e3eee4
add third
value: 35, address: 0x55dcb2e3eec0
value: 30, address: 0x55dcb2e3eec4
value: 25, address: 0x55dcb2e3eec8
Pop Back
value: 35, address: 0x55dcb2e3eec0
value: 30, address: 0x55dcb2e3eec4
add Fourth
value: 35, address: 0x55dcb2e3eec0
value: 30, address: 0x55dcb2e3eec4
value: 20, address: 0x55dcb2e3eec8
```

Here, we can see, after each `push_back`, a new array is created and item is added into it, and if there is any available space after `pop_back` new item will take its place.
