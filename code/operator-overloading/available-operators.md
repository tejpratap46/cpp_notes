# Available Operators

Not all operators are available for overloading, Here is a list of available operators for overloading.

**Arithmetic Operators:**

* `+` (addition)
* `-` (subtraction)
* `*` (multiplication)
* `/` (division)
* `%` (modulus)

**Assignment Operators:**

* `=` (assignment)
* `+=` (addition assignment)
* `-=` (subtraction assignment)
* `*=` (multiplication assignment)
* `/=` (division assignment)
* `%=` (modulus assignment)

**Comparison Operators:**  &#x20;

* `<` (less than)
* `>` (greater than)
* `<=` (less than or equal to)
* `>=` (greater than or equal to)
* `==` (equal to)
* `!=` (not equal to)

**Increment/Decrement Operators:**

* `++` (increment)
* `--` (decrement)

**Logical Operators:**

* `&&` (logical AND)
* `||` (logical OR)
* `!` (logical NOT)

**Bitwise Operators:**

* `&` (bitwise AND)
* `|` (bitwise OR)
* `^` (bitwise XOR)
* `~` (bitwise NOT)
* `<<` (left shift)
* `>>` (right shift)

**Member Access Operators:**

* `.` (dot operator)
* `->` (arrow operator)

**Subscript Operator:**

* `[]` (subscript operator)

**Function Call Operator:**

* `()` (function call operator)

**Comma Operator:**

* `,` (comma operator)

**New and Delete Operators:**

* `new` (memory allocation)
* `delete` (memory deallocation)

#### Important Notes

* You cannot overload operators for built-in types like `int`, `float`, etc.
* Overloaded operators must have at least one operand of user-defined type.
* The return type of an overloaded operator function is usually the same as the left-hand operand's type.
* Overloading can be done for both member functions and global functions.

By understanding these overloadable operators and their guidelines, you can effectively extend the behavior of your custom classes in C++.
