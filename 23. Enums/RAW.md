Enumerated types
================

Learn about the enum type in Dart.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/enums.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/enums&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/enums.md)

Enumerated types, often called _enumerations_ or _enums_, are a special kind of class used to represent a fixed number of constant values.

info Note

All enums automatically extend the [`Enum`](https://api.dart.dev/dart-core/Enum-class.html) class. They are also sealed, meaning they cannot be subclassed, implemented, mixed in, or otherwise explicitly instantiated.

Abstract classes and mixins can explicitly implement or extend `Enum`, but unless they are then implemented by or mixed into an enum declaration, no objects can actually implement the type of that class or mixin.

Declaring simple enums
----------------------

[#](https://dart.dev/language/enums#declaring-simple-enums)

To declare a simple enumerated type, use the `enum` keyword and list the values you want to be enumerated:

dart
```
enum Color { red, green, blue }
```
content_copy

lightbulb Tip

You can also use [trailing commas](https://dart.dev/language/collections#lists) when declaring an enumerated type to help prevent copy-paste errors.

Declaring enhanced enums
------------------------

[#](https://dart.dev/language/enums#declaring-enhanced-enums)

Dart also allows enum declarations to declare classes with fields, methods, and const constructors which are limited to a fixed number of known constant instances.

To declare an enhanced enum, follow a syntax similar to normal [classes](https://dart.dev/language/classes), but with a few extra requirements:

*    Instance variables must be `final`, including those added by [mixins](https://dart.dev/language/mixins). 
*    All [generative constructors](https://dart.dev/language/constructors#constant-constructors) must be constant. 
*   [Factory constructors](https://dart.dev/language/constructors#factory-constructors) can only return one of the fixed, known enum instances. 
*    No other class can be extended as [`Enum`](https://api.dart.dev/dart-core/Enum-class.html) is automatically extended. 
*    There cannot be overrides for `index`, `hashCode`, the equality operator `==`. 
*    A member named `values` cannot be declared in an enum, as it would conflict with the automatically generated static `values` getter. 
*    All instances of the enum must be declared in the beginning of the declaration, and there must be at least one instance declared. 

Instance methods in an enhanced enum can use `this` to reference the current enum value.

Here is an example that declares an enhanced enum with multiple instances, instance variables, getters, and an implemented interface:

dart
```
enum Vehicle implements Comparable<Vehicle> {
  car(tires: 4, passengers: 5, carbonPerKilometer: 400),
  bus(tires: 6, passengers: 50, carbonPerKilometer: 800),
  bicycle(tires: 2, passengers: 1, carbonPerKilometer: 0);
​
  const Vehicle({
    required this.tires,
    required this.passengers,
    required this.carbonPerKilometer,
  });
​
  final int tires;
  final int passengers;
  final int carbonPerKilometer;
​
  int get carbonFootprint => (carbonPerKilometer / passengers).round();
​
  bool get isTwoWheeled => this == Vehicle.bicycle;
​
  @override
  int compareTo(Vehicle other) => carbonFootprint - other.carbonFootprint;
}
```
content_copy

merge_type Version note

Enhanced enums require a [language version](https://dart.dev/resources/language/evolution#language-versioning) of at least 2.17.

Using enums
-----------

[#](https://dart.dev/language/enums#using-enums)

Access the enumerated values like any other [static variable](https://dart.dev/language/classes#class-variables-and-methods):

dart
```
final favoriteColor = Color.blue;
if (favoriteColor == Color.blue) {
  print('Your favorite color is blue!');
}
```
content_copy

Each value in an enum has an `index` getter, which returns the zero-based position of the value in the enum declaration. For example, the first value has index 0, and the second value has index 1.

dart
```
assert(Color.red.index == 0);
assert(Color.green.index == 1);
assert(Color.blue.index == 2);
```
content_copy

To get a list of all the enumerated values, use the enum's `values` constant.

dart
```
List<Color> colors = Color.values;
assert(colors[2] == Color.blue);
```
content_copy

You can use enums in [switch statements](https://dart.dev/language/branches#switch), and you'll get a warning if you don't handle all of the enum's values:

dart
```
var aColor = Color.blue;
​
switch (aColor) {
  case Color.red:
    print('Red as roses!');
  case Color.green:
    print('Green as grass!');
  default: // Without this, you see a WARNING.
    print(aColor); // 'Color.blue'
}
```
content_copy

If you need to access the name of an enumerated value, such as `'blue'` from `Color.blue`, use the `.name` property:

dart
```
print(Color.blue.name); // 'blue'
```
content_copy

You can access a member of an enum value like you would on a normal object:

dart
```
print(Vehicle.car.carbonFootprint);
```
content_copy
