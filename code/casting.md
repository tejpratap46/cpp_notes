# Casting

Here are 4 types of casting in cpp:

1. Static Cast (static\_cast\<new\_type>(expression))

* Purpose: Used for converting between related types.
* Safety: Relatively safe, as it performs compile-time type checking.
* Use cases:
  * Implicit conversions (e.g., int to float)
  * Explicit type conversions between related classes (up and down a class hierarchy)
  * Conversion between pointer types in a class hierarchy
* Checked at: Compile-time
*   Example:

    ```cpp
    double d = 3.14;
    int i = static_cast<int>(d);  // Converts double to int
    ```

2. Dynamic Cast (dynamic\_cast\<new\_type>(expression))

* Purpose: Used for safe downcasting in inheritance hierarchies.
* Safety: Very safe, as it performs runtime type checking.
* Use cases:
  * Converting pointers/references within an inheritance hierarchy
  * Determining runtime type information
* Checked at: Run-time
* Requires: At least one virtual function in the base class
*   Example:

    ```cpp
    class Base { virtual void foo() {} };
    class Derived : public Base { void bar() {} };

    Base* basePtr = new Derived;
    Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
    if (derivedPtr) {
        // Safe to use derivedPtr
    }
    ```

3. Const Cast (const\_cast\<new\_type>(expression))

* Purpose: To add or remove const/volatile qualifiers.
* Safety: Can be unsafe if misused, as it allows modification of const objects.
* Use cases:
  * Removing const-ness from objects that were originally non-const
  * Working with APIs that don't use const correctly
* Checked at: Compile-time
*   Example:

    ```cpp
    const int* constPtr = new int(10);
    int* mutablePtr = const_cast<int*>(constPtr);
    *mutablePtr = 20;  // Modifies the originally const value
    ```

4. Reinterpret Cast (reinterpret\_cast\<new\_type>(expression))

* Purpose: For low-level reinterpretation of bit patterns.
* Safety: Least safe, as it performs no checking and can easily lead to undefined behavior.
* Use cases:
  * Converting between unrelated pointer types
  * Converting between pointer and integer types
  * Bit manipulation
* Checked at: Compile-time (only for syntax, not for safety)
*   Example:

    ```cpp
    int i = 42;
    char* charPtr = reinterpret_cast<char*>(&i);
    ```

Key Differences:

1. Safety:
   * dynamic\_cast is the safest, with runtime checks.
   * static\_cast is next, with compile-time checks.
   * const\_cast is potentially unsafe if misused.
   * reinterpret\_cast is the least safe, with no real checks.
2. Purpose:
   * static\_cast is for general-purpose conversions.
   * dynamic\_cast is specifically for class hierarchies.
   * const\_cast is solely for const/volatile manipulation.
   * reinterpret\_cast is for low-level reinterpretation.
3. Runtime Overhead:
   * dynamic\_cast has the most overhead due to runtime type checking.
   * The others have minimal to no runtime overhead.
4. Compile-time vs. Runtime:
   * Only dynamic\_cast performs checks at runtime.
   * The others are resolved at compile-time.
5. Type Relationship:
   * static\_cast and dynamic\_cast work with related types.
   * const\_cast works only on cv-qualifiers.
   * reinterpret\_cast can work with completely unrelated types.

In general, it's best to use the most restrictive cast that accomplishes the task. static\_cast should be your go-to for most situations, dynamic\_cast when working with polymorphic types, const\_cast sparingly when absolutely necessary, and reinterpret\_cast only in very specific low-level scenarios.
