# Print memory



```cpp
#include <iostream>

void printMem(void *location)
{
    unsigned char const *pos = (unsigned char const *)location;

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
