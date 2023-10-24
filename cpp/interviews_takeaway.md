# Intervies Takeaway
## Virtual
First, some simple rules:
 - given a virtual method in a base class, each method with the same signature in derived classes will be virtual
 - a pure virtual method is a method that has no implementation: `virtual void test = 0`. Classes with this kind of methods cannot be instantiated.

`virtual` keyword changes the behaviour of the dispatcher. It enables dynamic dispatching (in constrast to default static one) for methods marked like that.

A dynamic dispatching means more overhead to solve the right method through the vtable of the class (more or less 5 `mov`, one `add` before the `call` instruction; results for x86 ISA).

Implementation-wise a vtable for each class that contains at least one `virtual` method is created; the vtable is always referred to the **class**. Each object references the vtable of its class by storing a pointer in a implicit extra attribute added by the compiler [constructor]. When a virtual method call [invocation] occurs, it is translated in:
 - `mov rax, QWORD PTR [rpb-24]` load obj address
 - `mov rax, QWORD PTR [rax]` load first attribute: vtable address
 - `add rax, 8` direct access to the right method in the table, since memory layout is known. Can be not there if the _first_ vmethod is what you need.
 - `mov rdx, QWORD PTR [rax]` dereference vmethod address
 - `mov rax, QWORD PTR [rpb-24]` reload obj address
 - `mov rdi, rax` put obj address in function (method) call firt position
 - `call rdx` calll the address solved 3 lines above

Apart from the implementation the idea is to allow method override. Without `virtual` when referencing to a child class through a partent class `Parent *x = new Child()` the methods of `Parent` are called, instead of the ones of `Child`, even if "overridden" (in this case is mere _redefinition_).

## Access modifiers
Enumerating them from the looser to the stricter:
 - `public` can be accesed by everyone
 - `protected` can be accesed by the class and its derivatives
 - `private` can be accesed only by class itself

```cpp
class Base {
    private:
        // ...
    protected:
        // ...
    public:
        // ...
}
```
Give `Base` class the following syntaxes are equivalent:
```cpp
class Derived : Base {}
```
and
```cpp
class Derived : public Base {}
```

Whereas `class Derived : protected Base {}` turns public methods and attributes into protected ones; and in turn `class Derived : private Base {}` turns all public and protected methods and attributes into provate ones. In general the access modifier for class derivation puts a limit on the access of base class members.


## Friends
Non-member functions and other classes' methods labeled as `friend` inside the class are allowed to manage private attributes. Member functions are implicitly friends.


