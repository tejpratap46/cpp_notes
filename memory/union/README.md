# ♻️ Union

In C++, a union is a special class type that allows you to store different data types in the same memory location. Here's a concise explanation of unions and their uses:

Definition: A union is a user-defined type where all members share the same memory location.

Key characteristics:

1. Only one member can hold a value at any given time.
2. The size of a union is determined by its largest member.

Main uses:

1. Memory optimisation: When you need to store different types of data, but never simultaneously, unions can save memory.
2. Type punning: Unions allow reinterpreting the same data as different types, though this can lead to undefined behaviour if not done carefully.
3. Interfacing with hardware: Unions are useful when working with low-level memory or hardware registers that can have multiple interpretations.

```cpp
union Punner {
    float f;
    int i;
};

Punner p;
p.f = 3.14f;
int bits = p.i;  // Access float's bit pattern as an int
```
