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

1. Here, we created 2 structs, Vector1
