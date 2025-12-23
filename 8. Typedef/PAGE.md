# Typedefs

A type alias—often called a _typedef_ because it's declared with the keyword `typedef`—is a concise way to refer to a type. Here's an example of declaring and using a type alias named `IntList`:

```dart
typedef IntList = List<int>;
IntList il = [1, 2, 3];
```

A type alias can have type parameters:

```dart
typedef ListMapper<X> = Map<X, List<X>>;
Map<String, List<String>> m1 = {}; // Verbose.
ListMapper<String> m2 = {}; // Same thing but shorter and clearer.
```

## Function Typedefs

We recommend using [inline function types](https://dart.dev/effective-dart/design#prefer-inline-function-types-over-typedefs) instead of typedefs for functions, in most situations. However, function typedefs can still be useful:

```dart
typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
```
