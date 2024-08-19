# Union, part 1

Union allows you to reuse a memory space for different-different data types, only one data can be stored at a time

Here is an example:

```cpp
#include <iostream>

union U
{
    int a;
    double b;
};

void printMem(void *location)
{
    unsigned char const *pos = (unsigned char const *)location;

    for (int i = 0; i < 20; i++)
        printf("|%2.2x| ", pos[i]);
    printf("\n");
}

int main(int argc, char const *argv[])
{
    U u1;

    u1.a = 3;
    std::cout << "a: " << u1.a << ", b: " << u1.b << std::endl;
    printMem(&u1);
    
    u1.b = 50;
    std::cout << "a: " << &u1.a << ", b: " << &u1.b << std::endl;
    printMem(&u1);

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42pm8suun):

Output:

```
a: 3, b: 6.95272e-310, size: 8
a: 0x7ffd9ee3ed90, b: 0x7ffd9ee3ed90, size: 8
|03| |00| |00| |00| |fd| |7f| |00| |00| |00| |3e| |6a| |2d| |2f| |ab| |1c| |8e| |00| |00| |00| |00| 
a: 0, b: 50, size: 8
a: 0x7ffd9ee3ed90, b: 0x7ffd9ee3ed90, size: 8
|00| |00| |00| |00| |00| |00| |49| |40| |00| |3e| |6a| |2d| |2f| |ab| |1c| |8e| |00| |00| |00| |00| 
```

Let' break down this example:

1. We create a simple union with 2 data inside, `a` as `integer` and `b` as `double`.
2. Once we store `a = 3` and print it, u1's memory addess will store 3 as a integer.
3. Now when we set `b = 50` and print it, u1's memory address will store 50 as a double.
4. And now if you try to read value of `a`, it will lose its value and will be overridden with byes of double (b).
5. Here we reused same memory location as different data types.
