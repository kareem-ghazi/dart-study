
// ...
}
```
content_copy

This also works with named variables.

dart
```
class PointC {
  double x; // must be set in constructor
  double y; // must be set in constructor
​
  // Generative constructor with initializing formal parameters
  // with default values
  PointC.named({this.x = 1.0, this.y = 1.0});
​
  @override
  String toString() {
    return 'PointC.named($x,$y)';
  }
}
​
// Constructor using named variables.
final pointC = PointC.named(x: 2.0, y: 2.0);
```
content_copy

All variables introduced from initializing formal parameters are both final and only in scope of the initialized variables.

To perform logic that you can't express in the initializer list, create a [factory constructor](https://dart.dev/language/constructors#factory-constructors) or [static method](https://dart.dev/language/classes#static-methods) with that logic. You can then pass the computed values to a normal constructor.

The constructor parameters could be set as nullable and not be initialized.

dart
```
class PointD {
  double? x; // null if not set in constructor
  double? y; // null if not set in constructor
​
  // Generative constructor with initializing formal parameters
  PointD(this.x, this.y);
​
  @override
  String toString() {
    return 'PointD($x,$y)';
  }
}
```
content_copy

### Use an initializer list

[#](https://dart.dev/language/constructors#use-an-initializer-list)

Before the constructor body runs, you can initialize instance variables. Separate initializers with commas.

dart
```
// Initializer list sets instance variables before
// the constructor body runs.
Point.fromJson(Map<String, double> json) : x = json['x']!, y = json['y']! {
  print('In Point.fromJson(): ($x, $y)');
}
```
content_copy

warning Warning

The right-hand side of an initializer list can't access `this`.

To validate inputs during development, use `assert` in the initializer list.

dart
```
Point.withAssert(this.x, this.y) : assert(x >= 0) {
  print('In Point.withAssert(): ($x, $y)');
}
```
content_copy

Initializer lists help set up `final` fields.

The following example initializes three `final` fields in an initializer list. To execute the code, click **Run**.

```
import 'dart:math';

class Point {
  final double x;
  final double y;
  final double distanceFromOrigin;

  Point(double x, double y)
    : x = x,
      y = y,
      distanceFromOrigin = sqrt(x * x + y * y);
}

void main() {
  var p = Point(2, 3);
  print(p.distanceFromOrigin);
}
```

Constructor inheritance
-----------------------

[#](https://dart.dev/language/constructors#constructor-inheritance)

_Subclasses_, or child classes, don't inherit _constructors_ from their _superclass_, or immediate parent class. If a class doesn't declare a constructor, it can only use the [default constructor](https://dart.dev/language/constructors#default-constructors).

A class can inherit the _parameters_ of a superclass. These are called [super parameters](https://dart.dev/language/constructors#super-parameters)

Constructors work in a somewhat similar way to how you call a chain of static methods. Each subclass can call its superclass's constructor to initialize an instance, like a subclass can call a superclass's static method. This process doesn't "inherit" constructor bodies or signatures.

### Non-default superclass constructors

[#](https://dart.dev/language/constructors#non-default-superclass-constructors)

Dart executes constructors in the following order:

1.   [initializer list](https://dart.dev/language/constructors#use-an-initializer-list)
2.   superclass's unnamed, no-arg constructor
3.   main class's no-arg constructor

If the superclass lacks an unnamed, no-argument constructor, call one of the constructors in the superclass. Before the constructor body (if any), specify the superclass constructor after a colon (`:`).

In the following example, the `Employee` class constructor calls the named constructor for its superclass, `Person`. To execute the following code, click **Run**.

```
class Person {
  String? firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson().
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

void main() {
  var employee = Employee.fromJson({});
  print(employee);
  // Prints:
  // in Person
  // in Employee
  // Instance of 'Employee'
}
```

As Dart evaluates the arguments to the superclass constructor _before_ invoking the constructor, an argument can be an expression like a function call.

dart
```
class Employee extends Person {
  Employee() : super.fromJson(fetchDefaultData());
  // ···
}
```
content_copy

warning Warning

Arguments to the superclass constructor can't access `this`. For example, arguments can call _static_ methods but not _instance_ methods.

### Super parameters

[#](https://dart.dev/language/constructors#super-parameters)

To avoid passing each parameter into the super invocation of a constructor, use super-initializer parameters to forward parameters to the specified or default superclass constructor. You can't use this feature with [redirecting constructors](https://dart.dev/language/constructors#redirecting-constructors). Super-initializer parameters have syntax and semantics like [initializing formal parameters](https://dart.dev/language/constructors#use-initializing-formal-parameters).

merge_type Version note

Using super-initializer parameters requires a [language version](https://dart.dev/resources/language/evolution#language-versioning) of at least 2.17. If you're using an earlier language version, you must manually pass in all super constructor parameters.

If the super-constructor invocation includes positional arguments, super-initializer parameters can't be positional.

dart
```
class Vector2d {
  final double x;
  final double y;
​
  Vector2d(this.x, this.y);
}
​
class Vector3d extends Vector2d {
  final double z;
​
  // Forward the x and y parameters to the default super constructor like:
  // Vector3d(final double x, final double y, this.z) : super(x, y);
  Vector3d(super.x, super.y, this.z);
}
```
content_copy

To further illustrate, consider the following example.

dart
```
// If you invoke the super constructor (`super(0)`) with any
  // positional arguments, using a super parameter (`super.x`)
  // results in an error.
  Vector3d.xAxisError(super.x): z = 0, super(0); // BAD
```
content_copy

This named constructor tries to set the `x` value twice: once in the super constructor and once as a positional super parameter. As both address the `x` positional parameter, this results in an error.

When the super constructor has named arguments, you can split them between named super parameters (`super.y` in the next example) and named arguments to the super constructor invocation (`super.named(x: 0)`).

dart
```
class Vector2d {
  // ...
  Vector2d.named({required this.x, required this.y});
}
​
class Vector3d extends Vector2d {
  final double z;
​
  // Forward the y parameter to the named super constructor like:
  // Vector3d.yzPlane({required double y, required this.z})
  //       : super.named(x: 0, y: y);
  Vector3d.yzPlane({required super.y, required this.z}) : super.named(x: 0);
}
```
content_copy