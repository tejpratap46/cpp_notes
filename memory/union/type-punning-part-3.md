# Type Punning, part 3

In last session, we read `struct` as a `array`, now we will extend on this with two struct implementation.

Here is what it would look like:

```cpp
#include <iostream>

struct Vector1
{
    int a, b;
};

struct Vector2
{
    int a, b, c, d;

    Vector1* getVector1() {
        // Return address of first element as Vector1
        return (Vector1*) &a;
    }
};

void printVector1(Vector1& vec1) {
    std::cout << vec1.a << ", " << vec1.b << std::endl;
}

int main(int argc, char const *argv[])
{
    Vector2 v2 = {1,2,3,4};
    
    Vector1* v1 = v2.getVector1();

    printVector1(v1[0]);
    printVector1(v1[1]);

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42p8pqnkh).

```cpp
// Output
1, 2
3, 4
```

Let's see how it works:

1. We have 2 structs, `Vector1` and `Vector2`.
2. `Vector1` contains 2 integers and `Vector2` constains 4 integers.
3. It can be said, `Vector2` can be read as **two** `Vector1` objects.
4. In the example above, we are doing the same thing. We create a object of `Vector2` that store 4 integer variables and then read them as two `Vector1` objects (as an array).
5. Thus, we successfully read a `Vector2` data as two `Vector1` data.
