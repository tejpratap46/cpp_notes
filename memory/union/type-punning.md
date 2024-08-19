# Type Punning

Type punning in C++ refers to the practice of accessing the same memory location as if it were a different data type than the one it was originally declared as. This technique allows you to interpret the binary representation of one data type as if it were another.

Here's a brief explanation of type punning:

1. Purpose: It's often used for low-level operations, like bit manipulation or when dealing with hardware interfaces.
2. Implementation: Typically done through pointer casting or unions.
3. Risks: It can lead to undefined behaviour if not used carefully, especially with strict aliasing rules.
4. Example: Converting between float and int without using conversion functions.

Here is a simple example:

```cpp
#include <iostream>

void printMem(void* location)
{
    unsigned char const *pos = (unsigned char const*) location;

    for (int i = 0; i < 20; i++)
        printf("|%2.2x| ", pos[i]);
    printf("\n");
}

int main(int argc, char const *argv[])
{
    double a = 2;
    std::cout << "a: " << a << ", address: " << &a << std::endl;
    printMem(&a);

    int b = *(int*)&a;

    std::cout << "b: " << b << ", address: " << &b << std::endl;
    printMem(&b);

    return 0;
}
```

> Try it [here](https://onecompiler.com/cpp/42p824qxx).

```
// Output
a: 2, address: 0x7ffc06b52220
|00| |00| |00| |00| |00| |00| |00| |40| |00| |60| |39| |68| |08| |fa| |4e| |3c| |00| |00| |00| |00| 
b: 0, address: 0x7ffc06b5221c
|00| |00| |00| |00| |00| |00| |00| |00| |00| |00| |00| |40| |00| |60| |39| |68| |08| |fa| |4e| |3c| 
```

In this example, you can see we

1. We stored `a` as double with value of `2`.
2. If you look at the memory output, double takes 8 bytes in memory. i.e.`|00| |00| |00| |00| |00| |00| |00| |40|` is double representation of value `2` in bytes.
3. Now, we read memory address of `a` and cast it as an integer pointer and store it in variable `b`.
4. Variable `b` is read as an integer, hence only 4 bytes will read instead of 8, which will be `|00| |00| |00| |00|`, hence will be read as `0`.
5. This is what type punning is, we are reading data as a different type.

> Note: `printMem()` function itself uses concepts of type punning to read memory as char and print on console.

Next, we will see how we can use this with structures.
