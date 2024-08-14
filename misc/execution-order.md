# Execution Order

Look at below example:

```cpp
#include <iostream>

using namespace std;

void printData(int a, int b) {
    cout << a << " + " << b << " = " << (a + b) << endl;
}

int main(int argc, char const *argv[])
{   
    int i = 0;
    printData(i++, ++i);
    return 0;
}
```

What will be the output, you have 4 options:

1. `1 + 2 = 3`
2. `0 + 0 = 0`
3. `0 + 1 = 1`
4. `1 + 0 = 1`

> Ans:
>
> This totally depends upon the compiler
