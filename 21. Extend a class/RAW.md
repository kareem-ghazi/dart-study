Extend a class
==============

Learn how to create subclasses from a superclass.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/extend.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/extend&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/extend.md)

Use `extends` to create a subclass, and `super` to refer to the superclass:

dart
```
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  // ···
}
​
class SmartTelevision extends Television {
  void turnOn() {
    super.turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  // ···
}
```
content_copy

For another usage of `extends`, see the discussion of [parameterized types](https://dart.dev/language/generics#restricting-the-parameterized-type) on the Generics page.

Overriding members
------------------

[#](https://dart.dev/language/extend#overriding-members)

Subclasses can override instance methods (including [operators](https://dart.dev/language/methods#operators)), getters, and setters. You can use the `@override` annotation to indicate that you are intentionally overriding a member:

dart
```
class Television {
  // ···
  set contrast(int value) {
    // ···
  }
}
​
class SmartTelevision extends Television {
  @override
  set contrast(num value) {
    // ···
  }
  // ···
}
```
content_copy

An overriding method declaration must match the method (or methods) that it overrides in several ways:

*    The return type must be the same type as (or a subtype of) the overridden method's return type. 
*    Parameter types must be the same type as (or a supertype of) the overridden method's parameter types. In the preceding example, the `contrast` setter of `SmartTelevision` changes the parameter type from `int` to a supertype, `num`. 
*    If the overridden method accepts _n_ positional parameters, then the overriding method must also accept _n_ positional parameters. 
*    A [generic method](https://dart.dev/language/generics#using-generic-methods) can't override a non-generic one, and a non-generic method can't override a generic one. 

Sometimes you might want to narrow the type of a method parameter or an instance variable. This violates the normal rules, and it's similar to a downcast in that it can cause a type error at runtime. Still, narrowing the type is possible if the code can guarantee that a type error won't occur. In this case, you can use the [`covariant` keyword](https://dart.dev/language/type-system#covariant-keyword) in a parameter declaration. For details, see the [Dart language specification](https://dart.dev/resources/language/spec).

warning Warning

If you override `==`, you should also override Object's `hashCode` getter. For an example of overriding `==` and `hashCode`, check out [Implementing map keys](https://dart.dev/libraries/dart-core#implementing-map-keys).

noSuchMethod()
--------------

[#](https://dart.dev/language/extend#nosuchmethod)

To detect or react whenever code attempts to use a non-existent method or instance variable, you can override `noSuchMethod()`:

dart
```
class A {
  // Unless you override noSuchMethod, using a
  // non-existent member results in a NoSuchMethodError.
  @override
  void noSuchMethod(Invocation invocation) {
    print(
      'You tried to use a non-existent member: '
      '${invocation.memberName}',
    );
  }
}
```
content_copy

You **can't invoke** an unimplemented method unless **one** of the following is true:

*   The receiver has the static type `dynamic`.

*   The receiver has a static type that defines the unimplemented method (abstract is OK), and the dynamic type of the receiver has an implementation of `noSuchMethod()` that's different from the one in class `Object`.

For more information, see the informal [noSuchMethod forwarding specification.](https://github.com/dart-lang/language/blob/main/archive/feature-specifications/nosuchmethod-forwarding.md)