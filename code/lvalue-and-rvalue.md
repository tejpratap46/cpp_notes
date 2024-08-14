---
icon: left-right
---

# LValue and RValue

Look at the below code:

```cpp
int b = 10;
```

Here, `b` is LValue and `10` is RValue. Take another example:

```cpp
#include <iostream>

int getValue() {
    return 40;
}

int main(int argc, char const *argv[])
{
    int b = 10;
    
    // getValue() = 30; // Not possible

    std::cout << "a: " << a << ", b: " << b << std::endl;

    return 0;
}
```

Here, we create a function, that will
