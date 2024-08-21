# Union, Part 2

Now, we lets move to a little complicated example with struct inside union with multiple size:

Here is a example:

```cpp
#include <iostream>

struct Vector1
{
    int a, b;
};

struct Vector2
{
    union
    {
        struct
        {
            int a,b,c,d;
        };
        struct
        {
            Vector1 x,y;
        };
    };
    
};

void printVector1(Vector1& v1) {
    std::cout << v1.a << ", " << v1.b << std::endl;
}

int main(int argc, char const *argv[])
{
    Vector2 v = {1,2,3,4};
    printVector1(v.x);
    printVector1(v.y);

    v.d = 500;
    printVector1(v.x);
    printVector1(v.y);

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42pm9r2ar):

Output:

```
1, 2
3, 4
1, 2
3, 500
```

Lets explore this example:

1. Here, we created 2 structs, `Vector1` and `Vector2`.
2. `Vector1` contains two integers: `a`, `b`.
3. `Vector2` contains two possible values based on union, either it will have four integers `a`, `b`, `c`, `d` or it will contain 2 `Vector1`.
4. Now, if we create an object of `Vector2` with values `{1, 2, 3, 4}`.
5. This `Vector2` instance can be converted into two instances of `Vector1` as it was part of the vector.
6. And, if we update a value of `Vector2` insrance and read it as `Vector1` Instance, you will see that `Vector1` data has been changes as they are referring to same memory location.
