# The Dart Type System

The Dart language is type safe: it uses a combination of static type checking and [runtime checks](https://dart.dev/language/type-system#runtime-checks) to ensure that a variable's value always matches the variable's static type, sometimes referred to as sound typing. Although _types_ are mandatory, type _annotations_ are optional because of [type inference](https://dart.dev/language/type-system#type-inference).

One benefit of static type checking is the ability to find bugs at compile time using Dart's [static analyzer.](https://dart.dev/tools/analysis)

You can fix most static analysis errors by adding type annotations to generic classes. The most common generic classes are the collection types `List<T>` and `Map<K,V>`.

For example, in the following code the `printInts()` function prints an integer list, and `main()` creates a list and passes it to `printInts()`.

```dart
void printInts(List<int> a) => print(a);

void main() {
  final list = [];
  list.add(1);
  list.add('2');
  printInts(list);
}
```

The preceding code results in a type error on `list` at the call of `printInts(list)`.

The error highlights an unsound implicit cast from `List<dynamic>` to `List<int>`. The `list` variable has static type `List<dynamic>`. This is because the initializing declaration `var list = []` doesn't provide the analyzer with enough information for it to infer a type argument more specific than `dynamic`. The `printInts()` function expects a parameter of type `List<int>`, causing a mismatch of types.

When adding a type annotation (`<int>`) on creation of the list the analyzer complains that a string argument can't be assigned to an `int` parameter. Removing the quotes in `list.add('2')` results in code that passes static analysis and runs with no errors or warnings.

```dart
void printInts(List<int> a) => print(a);

void main() {
  final list = <int>[];
  list.add(1);
  list.add(2);
  printInts(list);
}
```

## What is Soundness?

_Soundness_ is about ensuring your program can't get into certain invalid states. A sound _type system_ means you can never get into a state where an expression evaluates to a value that doesn't match the expression's static type. For example, if an expression's static type is `String`, at runtime you are guaranteed to only get a string when you evaluate it.

Dart's type system, like the type systems in Java and C#, is sound. It enforces that soundness using a combination of static checking (compile-time errors) and runtime checks. For example, assigning a `String` to `int` is a compile-time error. Casting an object to a `String` using `as String` fails with a runtime error if the object isn't a `String`.

## The Benefits of Soundness

A sound type system has several benefits:

*   **Revealing type-related bugs at compile time.** A sound type system forces code to be unambiguous about its types, so type-related bugs that might be tricky to find at runtime are revealed at compile time.
*   **More readable code.** Code is easier to read because you can rely on a value actually having the specified type. In sound Dart, types can't lie.
*   **More maintainable code.** With a sound type system, when you change one piece of code, the type system can warn you about the other pieces of code that just broke.
*   **Better ahead of time (AOT) compilation.** While AOT compilation is possible without types, the generated code is much less efficient.

## Tips for Passing Static Analysis

Most of the rules for static types are easy to understand. Here are some of the less obvious rules:

*   Use sound return types when overriding methods.
*   Use sound parameter types when overriding methods.
*   Don't use a dynamic list as a typed list.

### Use Sound Return Types When Overriding Methods

The return type of a method in a subclass must be the same type or a subtype of the return type of the method in the superclass. Consider the getter method in the `Animal` class:

```dart
class Animal {
  void chase(Animal a) {
     // ...
  }
  Animal get parent => ...
}
```

The `parent` getter method returns an `Animal`. In the `HoneyBadger` subclass, you can replace the getter's return type with `HoneyBadger` (or any other subtype of `Animal`), but an unrelated type is not allowed.

```dart
class HoneyBadger extends Animal {
  @override
  void chase(Animal a) {
     // ...
  }

  @override
  HoneyBadger get parent => ...
}
```

### Use Sound Parameter Types When Overriding Methods

The parameter of an overridden method must have either the same type or a supertype of the corresponding parameter in the superclass. Don't "tighten" the parameter type by replacing the type with a subtype of the original parameter.

**Note:** If you have a valid reason to use a subtype, you can use the [`covariant` keyword](https://dart.dev/language/type-system#covariant-keyword).

Consider the `chase(Animal)` method for the `Animal` class:

```dart
class Animal {
  void chase(Animal a) {
     // ...
  }
  Animal get parent => ...
}
```

The `chase()` method takes an `Animal`. A `HoneyBadger` chases anything. It's OK to override the `chase()` method to take anything (`Object`).

```dart
class HoneyBadger extends Animal {
  @override
  void chase(Object a) {
     // ...
  }

  @override
  Animal get parent => ...
}
```

## Runtime Checks

Runtime checks deal with type safety issues that can't be detected at compile time.

For example, the following code throws an exception at runtime because it's an error to cast a list of dogs to a list of cats:

```dart
void main() {
  List<Animal> animals = <Dog>[Dog()];
  List<Cat> cats = animals as List<Cat>;
}
```

### Implicit Downcasts from `dynamic`

Expressions with a static type of `dynamic` can be implicitly cast to a more specific type. If the actual type doesn't match, the cast throws an error at run time.

```dart
int assumeString(dynamic object) {
  String string = object; // Check at run time that `object` is a `String`.
  return string.length;
}
```

## Type Inference

The analyzer can infer types for fields, methods, local variables, and most generic type arguments. When the analyzer doesn't have enough information to infer a specific type, it uses the `dynamic` type.

Here's an example of how type inference works with generics. In this example, a variable named `arguments` holds a map that pairs string keys with values of various types.

If you explicitly type the variable, you might write this:

```dart
Map<String, Object?> arguments = {'argA': 'hello', 'argB': 42};
```

Alternatively, you can use `var` or `final` and let Dart infer the type:

```dart
var arguments = {'argA': 'hello', 'argB': 42}; // Map<String, Object>
```

## Covariant Parameters

Some (rarely used) coding patterns rely on tightening a type by overriding a parameter's type with a subtype, which is invalid. In this case, you can use the `covariant` keyword to tell the analyzer that you're doing this intentionally. This removes the static error and instead checks for an invalid argument type at runtime.

The following shows how you might use `covariant`:

```dart
class Animal {
  void chase(Animal x) {
     // ...
  }
}

class Mouse extends Animal {
   // ...
}

class Cat extends Animal {
  @override
  void chase(covariant Mouse x) {
     // ...
  }
}
```
