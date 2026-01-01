Mixins
======

Learn how to add to features to a class in Dart.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/mixins.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/mixins&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/mixins.md)

Mixins are a way of defining code that can be reused in multiple class hierarchies. They are intended to provide member implementations en masse.

To use a mixin, use the `with` keyword followed by one or more mixin names. The following example shows two classes that use (or, are subclasses of) mixins:

dart
```
class Musician extends Performer with Musical {
  // ···
}
​
class Maestro extends Person with Musical, Aggressive, Demented {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
```
content_copy

To define a mixin, use the `mixin` declaration. In the rare case where you need to define both a mixin _and_ a class, you can use the [`mixin class` declaration](https://dart.dev/language/mixins#class-mixin-or-mixin-class).

Mixins and mixin classes cannot have an `extends` clause, and must not declare any generative constructors.

For example:

dart
```
mixin Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;
​
  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
```
content_copy

Specify members a mixin can call on itself
------------------------------------------

[#](https://dart.dev/language/mixins#specify-members-a-mixin-can-call-on-itself)

Sometimes a mixin depends on being able to invoke a method or access fields, but can't define those members itself (because mixins can't use constructor parameters to instantiate their own fields).

The following sections cover different strategies for ensuring any subclass of a mixin defines any members the mixin's behavior depends on.

### Define abstract members in the mixin

[#](https://dart.dev/language/mixins#define-abstract-members-in-the-mixin)

Declaring an abstract method in a mixin forces any type that uses the mixin to define the abstract method upon which its behavior depends.

dart
```
mixin Musician {
  void playInstrument(String instrumentName); // Abstract method.
​
  void playPiano() {
    playInstrument('Piano');
  }
  void playFlute() {
    playInstrument('Flute');
  }
}
​
class Virtuoso with Musician {
​
  @override
  void playInstrument(String instrumentName) { // Subclass must define.
    print('Plays the $instrumentName beautifully');
  }
}
```
content_copy

#### Access state in the mixin's subclass

[#](https://dart.dev/language/mixins#access-state-in-the-mixins-subclass)

Declaring abstract members also allows you to access state on the subclass of a mixin, by calling getters which are defined as abstract on the mixin:

dart
```
/// Can be applied to any type with a [name] property and provides an
/// implementation of [hashCode] and operator `==` in terms of it.
mixin NameIdentity {
  String get name;
​
  @override
  int get hashCode => name.hashCode;
​
  @override
  bool operator ==(other) => other is NameIdentity && name == other.name;
}
​
class Person with NameIdentity {
  final String name;
​
  Person(this.name);
}
```
content_copy

### Implement an interface

[#](https://dart.dev/language/mixins#implement-an-interface)

Similar to declaring the mixin abstract, putting an `implements` clause on the mixin while not actually implementing the interface will also ensure any member dependencies are defined for the mixin.

dart
```
abstract interface class Tuner {
  void tuneInstrument();
}
​
mixin Guitarist implements Tuner {
  void playSong() {
    tuneInstrument();
​
    print('Strums guitar majestically.');
  }
}
​
class PunkRocker with Guitarist {
​
  @override
  void tuneInstrument() {
    print("Don't bother, being out of tune is punk rock.");
  }
}
```
content_copy

### Use the `on` clause to declare a superclass

[#](https://dart.dev/language/mixins#use-the-on-clause-to-declare-a-superclass)

The `on` clause exists to define the type that `super` calls are resolved against. So, you should only use it if you need to have a `super` call inside a mixin.

The `on` clause forces any class that uses a mixin to also be a subclass of the type in the `on` clause. If the mixin depends on members in the superclass, this ensures those members are available where the mixin is used:

dart
```
class Musician {
  musicianMethod() {
    print('Playing music!');
  }
}
​
mixin MusicalPerformer on Musician {
  performerMethod() {
    print('Performing music!');
    super.musicianMethod();
  }
}
​
class SingerDancer extends Musician with MusicalPerformer { }
​
main() {
  SingerDancer().performerMethod();
}
```
content_copy

In this example, only classes that extend or implement the `Musician` class can use the mixin `MusicalPerformer`. Because `SingerDancer` extends `Musician`, `SingerDancer` can mix in `MusicalPerformer`.

`class`, `mixin`, or `mixin class`?
-----------------------------------

[#](https://dart.dev/language/mixins#class-mixin-or-mixin-class)

merge_type Version note

The `mixin class` declaration requires a [language version](https://dart.dev/resources/language/evolution#language-versioning) of at least 3.0.

A `mixin` declaration defines a mixin. A `class` declaration defines a [class](https://dart.dev/language/classes). A `mixin class` declaration defines a class that is usable as both a regular class and a mixin, with the same name and the same type.

dart
```
mixin class Musician {
  // ...
}
​
class Novice with Musician { // Use Musician as a mixin
  // ...
}
​
class Novice extends Musician { // Use Musician as a class
  // ...
}
```
content_copy

Any restrictions that apply to classes or mixins also apply to mixin classes:

*    Mixins can't have `extends` or `with` clauses, so neither can a `mixin class`. 
*   Classes can't have an `on` clause, so neither can a `mixin class`.