# Public vs Private inheritance

Public and private inheritance are important concepts in C++ that affect how the members of a base class are accessed in the derived class.

1. Public Inheritance:
   * Syntax: `class Derived : public Base`
   * Public members of the base class remain public in the derived class.
   * Protected members of the base class remain protected in the derived class.
   * Private members of the base class remain inaccessible in the derived class.
   * Preserves the "is-a" relationship between base and derived classes.
2. Private Inheritance:
   * Syntax: `class Derived : private Base`
   * Public and protected members of the base class become private in the derived class.
   * Private members of the base class remain inaccessible in the derived class.
   * Often used to implement a "has-a" relationship.

Here's a simple example to illustrate these concepts:

```cpp
class Base {
public:
    int publicVar;
protected:
    int protectedVar;
private:
    int privateVar;
};

class PublicDerived : public Base {
    // publicVar is public
    // protectedVar is protected
    // privateVar is not accessible
};

class PrivateDerived : private Base {
    // publicVar is private
    // protectedVar is private
    // privateVar is not accessible
};

int main() {
    PublicDerived pub;
    pub.publicVar = 1;  // OK
    // pub.protectedVar = 2;  // Error: protected
    // pub.privateVar = 3;    // Error: private

    PrivateDerived priv;
    // priv.publicVar = 1;    // Error: private in PrivateDerived
    // priv.protectedVar = 2; // Error: private in PrivateDerived
    // priv.privateVar = 3;   // Error: not accessible

    return 0;
}
```

Key points to remember:

1. With public inheritance, the public interface of the base class becomes part of the public interface of the derived class.
2. With private inheritance, all members of the base class become private in the derived class, regardless of their original access level.
3. Private inheritance is often used when you want to use the implementation of a base class but not inherit its interface.
4. Public inheritance models an "is-a" relationship (e.g., a Dog is an Animal), while private inheritance often models a "has-a" or "is-implemented-in-terms-of" relationship.
