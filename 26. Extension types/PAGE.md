# Extension types

An extension type is a compile-time abstraction that "wraps" an existing type with a different, static-only interface. They are a major component of static JS interop because they can easily modify an existing type's interface without incurring the cost of an actual wrapper.

Extension types enforce discipline on the set of operations (or interface) available to objects of an underlying type, called the _representation type_.

## Syntax

Define a new extension type with the `extension type` declaration and a name, followed by the representation type declaration in parentheses:

```dart
extension type E(int i) {
  // Define set of operations.
}
```

The representation type declaration `(int i)` specifies that the underlying type of extension type `E` is `int`. It introduces:
*   An implicit getter `int get i`.
*   An implicit constructor `E(int i) : i = i`.

You can optionally declare constructors in an extension type's body.

```dart
extension type E(int i) {
  E.n(this.i);
  E.m(int j, String foo) : i = j + foo.length;
}

void main() {
  E(4); // Implicit unnamed constructor.
  E.n(3); // Named constructor.
  E.m(5, "Hello!"); // Named constructor with additional parameters.
}
```

## Declaring members

Declare members in the body of an extension type to define its interface. Extension type members can be methods, getters, setters, or operators (non-external instance variables and abstract members are not allowed):

```dart
extension type NumberE(int value) {
  // Operator:
  NumberE operator +(NumberE other) =>
      NumberE(value + other.value);
  // Getter:
  NumberE get myNum => this;
  // Method:
  bool isValid() => !value.isNegative;
}
```

## Implements clause

Interface members of the representation type are not interface members of the extension type by default.

You can optionally use the `implements` clause to:
*   Introduce a subtype relationship on an extension type.
*   Add the members of the representation object to the extension type interface.

```dart
extension type NumberI(int i) implements int {
  // 'NumberI' can invoke all members of 'int',
  // plus anything else it declares here.
}
```

## Core use cases

There are two equally valid, but substantially different core use cases for extension types:

1.  **Providing an extended interface:** When an extension type implements its representation type, it is "transparent". It sees the underlying type's members plus any new ones.
2.  **Providing a different interface:** An extension type that is not transparent is treated statically as a completely new type. This is useful for type safety (e.g., `IdNumber` vs `int`).

```dart
extension type IdNumber(int id) {
  operator <(IdNumber other) => id < other.id;
}

void main() {
  int myUnsafeId = 42424242;
  myUnsafeId = myUnsafeId + 10; // Unsafe, but allowed for int.

  var safeId = IdNumber(42424242);
  // safeId + 10; // Error: No '+' operator defined.
  safeId < IdNumber(42424241); // OK.
}
```

## Type considerations

Extension types are a **compile-time wrapping construct**. At run time, there is absolutely no trace of the extension type. Any type query (`is`, `as`, `runtimeType`) works on the representation type.

```dart
void main() {
  var n = NumberE(1);

  // The run-time type of 'n' is the representation type 'int'.
  if (n is int) print(n); // Prints 1.
}
```

This makes extension types an _unsafe_ abstraction because you can always cast to the underlying type at runtime. However, they provide excellent performance as they are erased during compilation.
