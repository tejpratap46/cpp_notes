# Function Pointer

With function pointer, we can point to a function implementation with same signature to be executed when referenced.

```cpp
#include <iostream>

int double_value(int x) {
  return x * 2;
}

void map(int *arr, int size, int (*func)(int)) {
  for (int i = 0; i < size; i++) {
    arr[i] = func(arr[i]);
  }
}

int main() {
  int numbers[] = {1, 2, 3, 4, 5};
  int size = sizeof(numbers) / sizeof(numbers[0]);

  map(numbers, size, double_value);

  for (int i = 0; i < size; i++) {
    printf("%d ", numbers[i]);
  }
  printf("\n");

  return 0;
}
```

Run it [here](https://onecompiler.com/cpp/42kzwj4pv).
