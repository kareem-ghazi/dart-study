Dart 3.10 is taking off with dot shorthands, stable build hooks, nuanced deprecation annotations, and more! [Learn more](https://blog.dart.dev/announcing-dart-3-10-ea8b952b6088)

1.   [Language](https://dart.dev/language)
2.   [Class modifiers](https://dart.dev/language/class-modifiers)

Modifier keywords for class declarations to control external library access.

Class modifiers control how a class or mixin can be used, both [from within its own library](https://dart.dev/language/class-modifiers#abstract), and from outside the library where it's defined.

Modifier keywords come before a class or mixin declaration. For example, writing `abstract class` defines an abstract class. The full set of modifiers that can appear before a class declaration include:

*   `abstract`
*   `base`
*   `final`
*   `interface`
*   `sealed`
*   [`mixin`](https://dart.dev/language/mixins#class-mixin-or-mixin-class)

Only the `base` modifier can appear before a mixin declaration. The modifiers do not apply to other declarations like `enum`, `typedef`, `extension`, or `extension type`.

When deciding whether to use class modifiers, consider the intended uses of the class and what behaviors the class needs to be able to rely on.

To allow unrestricted permission to construct or subtype from any library, use a `class` or `mixin` declaration without a modifier. By default, you can:

*   [Construct](https://dart.dev/language/constructors) new instances of a class.
*   [Extend](https://dart.dev/language/extend) a class to create a new subtype.
*   [Implement](https://dart.dev/language/classes#implicit-interfaces) a class or mixin's interface.
*   [Mix in](https://dart.dev/language/mixins) a mixin or mixin class.

To define a class that doesn't require a full, concrete implementation of its entire interface, use the `abstract` modifier.

Abstract classes cannot be constructed from any library, whether its own or an outside library. Abstract classes often have [abstract methods](https://dart.dev/language/methods#abstract-methods).

a.dart

dart

```
abstract class Vehicle {
  void moveForward(int meters);
}
```

b.dart

dart

```
import 'a.dart';
​
// Error: `Vehicle` can't be instantiated because
// it is marked as `abstract`.
Vehicle myVehicle = Vehicle();
​
// Can be extended.
class Car extends Vehicle {
  int passengers = 4;
​
  @override
  void moveForward(int meters) {
    // ...
  }
}
​
// Can be implemented.
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
    // ...
  }
}
```

If you want your abstract class to appear to be instantiable, define a [factory constructor](https://dart.dev/language/constructors#factory-constructors).

To enforce inheritance of a class or mixin's implementation, use the `base` modifier. A base class disallows implementation outside of its own library. This guarantees:

*    The base class constructor is called whenever an instance of a subtype of the class is created. 
*   All implemented private members exist in subtypes.
*    A new implemented member in a `base` class does not break subtypes, since all subtypes inherit the new member.
    *   This is true unless the subtype already declares a member with the same name and an incompatible signature.

You must mark any class that implements or extends a base class as `base`, `final`, or `sealed`. This prevents outside libraries from breaking the base class guarantees.

a.dart

dart

```
base class Vehicle {
  void moveForward(int meters) {
    // ...
  }
}
```

b.dart

dart

```
import 'a.dart';
​
// Can be constructed.
Vehicle myVehicle = Vehicle();
​
// Can be extended.
base class Car extends Vehicle {
  int passengers = 4;
  // ...
}
​
// ERROR: `Vehicle` can't be implemented in a different library because
// it is marked with `base`.
base class MockVehicle implements Vehicle {
  @override
  void moveForward() {
    // ...
  }
}
```

To define an interface, use the `interface` modifier. Libraries outside of the interface's own defining library can implement the interface, but not extend it. This guarantees:

*    When one of the class's instance methods calls another instance method on `this`, it will always invoke a known implementation of the method from the same library. 
*    Other libraries can't override methods that the interface class's own methods might later call in unexpected ways. This reduces the [fragile base class problem](https://en.wikipedia.org/wiki/Fragile_base_class). 

a.dart

dart

```
interface class Vehicle {
  void moveForward(int meters) {
    // ...
  }
}
```

b.dart

dart

```
import 'a.dart';
​
// Can be constructed.
Vehicle myVehicle = Vehicle();
​
// ERROR: `Vehicle` can't be extended in a different library because
// it is marked with `interface`.
class Car extends Vehicle {
  int passengers = 4;
  // ...
}
​
// Can be implemented.
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
    // ...
  }
}
```

### `abstract interface`

[#](https://dart.dev/language/class-modifiers#abstract-interface)

The most common use for the `interface` modifier is to define a pure interface. [Combine](https://dart.dev/language/class-modifiers#combining-modifiers) the `interface` and [`abstract`](https://dart.dev/language/class-modifiers#abstract) modifiers for an `abstract interface class`.

Like an `interface` class, other libraries can implement, but can't inherit, a pure interface. Like an `abstract` class, a pure interface can have abstract members.

To close the type hierarchy, use the `final` modifier. This prevents subtyping from a class outside of the current library. Disallowing both inheritance and implementation prevents subtyping entirely. This guarantees:

*   You can safely add incremental changes to the API.
*    You can call instance methods knowing that they haven't been overwritten in a third-party subclass. 

Final classes can be extended or implemented within the same library. The `final` modifier encompasses the effects of `base`, and therefore any subclasses must also be marked `base`, `final`, or `sealed`.

a.dart

dart

```
final class Vehicle {
  void moveForward(int meters) {
    // ...
  }
}
```

b.dart

dart

```
import 'a.dart';
​
// Can be constructed.
Vehicle myVehicle = Vehicle();
​
// ERROR: `Vehicle` can't be extended in a different library
// because it is marked `final`.
class Car extends Vehicle {
  int passengers = 4;
  // ...
}
​
// ERROR: `Vehicle` can't be implemented in a different library because
// it is marked `final`.
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
    // ...
  }
}
```

To create a known, enumerable set of subtypes, use the `sealed` modifier. This allows you to create a switch over those subtypes that is statically ensured to be [_exhaustive_](https://dart.dev/language/branches#exhaustiveness-checking).

The `sealed` modifier prevents a class from being extended or implemented outside its own library. Sealed classes are implicitly [abstract](https://dart.dev/language/class-modifiers#abstract).

*   They cannot be constructed themselves.
*   They can have [factory constructors](https://dart.dev/language/constructors#factory-constructors).
*   They can define constructors for their subclasses to use.

Subclasses of sealed classes are, however, not implicitly abstract.

The compiler is aware of any possible direct subtypes because they can only exist in the same library. This allows the compiler to alert you when a switch does not exhaustively handle all possible subtypes in its cases:

dart

```
sealed class Vehicle {}
​
class Car extends Vehicle {}
​
class Truck implements Vehicle {}
​
class Bicycle extends Vehicle {}
​
// ERROR: `Vehicle` can't be instantiated because
// it is marked `sealed` and therefore, implicitly abstract.
Vehicle myVehicle = Vehicle();
​
// Subclasses of a sealed class can be instantiated unless also restricted.
Vehicle myCar = Car();
​
extension VehicleSounds on Vehicle {
  String get sound {
    // ERROR: The switch does not exhaustively account for
    // all possible objects of type `Vehicle`.
    // In this example, a `Vehicle` with a run-time type of `Bicycle`
    // would not match any of the cases.
    return switch (this) {
      Car() => 'vroom',
      Truck() => 'VROOOOMM',
    };
  }
}
```

If you don't want [exhaustive switching](https://dart.dev/language/branches#exhaustiveness-checking), or want to be able to add subtypes later without breaking the API, use the [`final`](https://dart.dev/language/class-modifiers#final) modifier. For a more in depth comparison, read [`sealed` versus `final`](https://dart.dev/language/class-modifiers-for-apis#sealed-versus-final).

Combining modifiers
-------------------

[#](https://dart.dev/language/class-modifiers#combining-modifiers)

You can combine some modifiers for layered restrictions. A class declaration can be, in order:

1.    (Optional) `abstract`, describing whether the class can contain abstract members and prevents instantiation. 
2.    (Optional) One of `base`, `interface`, `final` or `sealed`, describing restrictions on other libraries subtyping the class. 
3.   (Optional) `mixin`, describing whether the declaration can be mixed in.
4.   The `class` keyword itself.

You can't combine some modifiers because they are contradictory, redundant, or otherwise mutually exclusive:

*   `abstract` with `sealed`. A [sealed](https://dart.dev/language/class-modifiers#sealed) class is implicitly [abstract](https://dart.dev/language/class-modifiers#abstract). 
*   `interface`, `final` or `sealed` with `mixin`. These access modifiers prevent [mixing in](https://dart.dev/language/mixins). 

For further guidance on how class modifiers can be combined, check out the [Class modifiers reference](https://dart.dev/language/modifier-reference).