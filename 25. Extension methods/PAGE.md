# Extension methods

Extension methods add functionality to existing libraries. You might use extension methods without even knowing it. For example, when you use code completion in an IDE, it suggests extension methods alongside regular methods.

When you're using someone else's API or when you implement a library that's widely used, it's often impractical or impossible to change the API. But you might still want to add some functionality.

For example, consider the following code that parses a string into an integer:

```dart
int.parse('42')
```

It might be nice—shorter and easier to use with tools—to have that functionality be on `String` instead:

```dart
'42'.parseInt()
```

To enable that code, you can import a library that contains an extension of the `String` class:

```dart
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }
}

void main() {
  print('42'.parseInt()); // Use an extension method.
}
```

Extensions can define not just methods, but also other members such as getter, setters, and operators. Also, extensions can have names, which can be helpful if an API conflict arises.

## Using extension methods

Like all Dart code, extension methods are in libraries. You've already seen how to use an extension method—just import the library it's in, and use it like an ordinary method:

```dart
void main() {
  print('42'.parseInt()); // Use an extension method.
}
```

### Static types and dynamic

You can't invoke extension methods on variables of type `dynamic`. For example, the following code results in a runtime exception:

```dart
dynamic d = '2';
print(d.parseInt()); // Runtime exception: NoSuchMethodError
```

The reason that `dynamic` doesn't work is that extension methods are resolved against the static type of the receiver. Because extension methods are resolved statically, they're as fast as calling a static function.

### API conflicts

If an extension member conflicts with an interface or with another extension member, then you have a few options.

One option is changing how you import the conflicting extension, using `show` or `hide` to limit the exposed API.

Another option is applying the extension explicitly, which results in code that looks as if the extension is a wrapper class:

```dart
// Both libraries define extensions on String that contain parseInt(),
// and the extensions have different names.
// import 'string_apis.dart'; // Contains NumberParsing extension.
// import 'string_apis_2.dart'; // Contains NumberParsing2 extension.

void main() {
  // print('42'.parseInt()); // Doesn't work if ambiguous.
  print(NumberParsing('42').parseInt());
  print(NumberParsing2('42').parseInt());
}
```

## Implementing extension methods

Use the following syntax to create an extension:

```dart
extension <extension name>? on <type> { // <extension-name> is optional
  (<member definition>)* // Can provide one or more <member definition>.
}
```

For example, here's how you might implement an extension on the `String` class:

```dart
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }

  double parseDouble() {
    return double.parse(this);
  }
}
```

The members of an extension can be methods, getters, setters, or operators. Extensions can also have static fields and static helper methods.

### Unnamed extensions

When declaring an extension, you can omit the name. Unnamed extensions are visible only in the library where they're declared. Since they don't have a name, they can't be explicitly applied to resolve API conflicts.

```dart
extension on String {
  bool get isBlank => trim().isEmpty;
}
```

## Implementing generic extensions

Extensions can have generic type parameters. For example, here's some code that extends the built-in `List<T>` type with a getter, an operator, and a method:

```dart
extension MyFancyList<T> on List<T> {
  int get doubleLength => length * 2;
  List<T> operator -() => reversed.toList();
  List<List<T>> split(int at) => [sublist(0, at), sublist(at)];
}
```

The type `T` is bound based on the static type of the list that the methods are called on.
