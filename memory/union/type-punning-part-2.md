# Type Punning, part 2

In last session, we converted `double` to `int`, now we will extend on this with a struct implementation.

Here is what it would look like:

```cpp
#include <iostream>

struct Vector
{
    int a, b;
};

void printMem(void *location)
{
    unsigned char const *pos = (unsigned char const *)location;

    for (int i = 0; i < 20; i++) {
        printf("|%2.2x| ", pos[i]);
    }
    
    printf("\n");
}

int main(int argc, char const *argv[])
{
    Vector v = {1 ,2};
    printMem(&v);

    int* v2 = (int*) &v;
    std::cout << "a: " << v2[0] << ", b: " << v2[1] << std::endl;

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42pf8ja3v).

```cpp
// Output
|01| |00| |00| |00| |02| |00| |00| |00| |00| |26| |87| |5e| |29| |fe| |f1| |3b| |00| |00| |00| |00| 
a: 1, b: 2
```

Let's see how it works:

1. We have a structs, `Vector`.
2. `Vector` contains 2 integers `a` and `b`.
3. If we look at its memory allocation, it would be similar to an array with two int.
4. It means, we can read this struct as an array with indexes.
5. Hence, if we get pointer to `a` in struct, we can index on it to read value of `b` from its memory.
