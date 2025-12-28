1.   [Language](https://dart.dev/language)
2.   [Metadata](https://dart.dev/language/metadata)

Metadata and annotations in Dart.

Use metadata to provide additional static information about your code. A metadata annotation begins with the character `@`, followed by either a reference to a compile-time constant (such as `deprecated`) or a call to a constant constructor.

Metadata can be attached to most Dart program constructs by adding annotations before the construct's declaration or directive.

Built-in annotations
--------------------

[#](https://dart.dev/language/metadata#built-in-annotations)

The following annotations are available to all Dart code:

[`@Deprecated`](https://api.dart.dev/dart-core/Deprecated-class.html)
Marks a declaration as deprecated, indicating it should be migrated away from, with a message explaining the replacement and potential removal date.

In addition to the general `@Deprecated` annotation, you can use specific annotations to deprecate certain usages of a declaration:

*   [`@Deprecated.extend()`](https://api.dart.dev/beta/latest/dart-core/Deprecated/Deprecated.extend.html): Extending the class is deprecated. 
*   [`@Deprecated.implement()`](https://api.dart.dev/beta/latest/dart-core/Deprecated/Deprecated.implement.html): Implementing the class or mixin is deprecated. 
*   [`@Deprecated.subclass()`](https://api.dart.dev/beta/latest/dart-core/Deprecated/Deprecated.subclass.html): Subclassing (extending or implementing) the class or mixin is deprecated. 
*   [`@Deprecated.mixin()`](https://api.dart.dev/beta/latest/dart-core/Deprecated/Deprecated.mixin.html): Mixing in the class is deprecated. 
*   [`@Deprecated.instantiate()`](https://api.dart.dev/beta/latest/dart-core/Deprecated/Deprecated.instantiate.html): Instantiating the class is deprecated. 
*   [`@Deprecated.optional()`](https://api.dart.dev/beta/latest/dart-core/Deprecated/Deprecated.optional.html): Omitting an argument for the parameter is deprecated. 

Here's an example of using the `@Deprecated` annotation:

dart

```
class Television {
  /// Use [turnOn] to turn the power on instead.
  @Deprecated('Use turnOn instead')
  void activate() {
    turnOn();
  }
​
  /// Turns the TV's power on.
  void turnOn() {
    // ···
  }
  // ···
}
```

[`@deprecated`](https://api.dart.dev/dart-core/Deprecated-class.html)
Marks a declaration as deprecated until an unspecified future release. Prefer using `@Deprecated` and [providing a deprecation message](https://dart.dev/tools/linter-rules/provide_deprecation_message).

[`@override`](https://api.dart.dev/dart-core/override-constant.html)
Marks an instance member as an override or implementation of a member with the same name from a parent class or interface. For examples of using `@override`, check out [Extend a class](https://dart.dev/language/extend).

[`@pragma`](https://api.dart.dev/dart-core/pragma-class.html)
Provides specific instructions or hints about a declaration to Dart tools, such as the compiler or analyzer.

The [Dart analyzer](https://dart.dev/tools/analysis) provides feedback as diagnostics if the `@override` annotation is needed and when using members annotated with `@deprecated` or `@Deprecated`.

Analyzer-supported annotations
------------------------------

[#](https://dart.dev/language/metadata#analyzer-supported-annotations)

Beyond providing support and analysis for the [built-in annotations](https://dart.dev/language/metadata#built-in-annotations), the [Dart analyzer](https://dart.dev/tools/analysis) provides additional support and diagnostics for a variety of annotations from [`package:meta`](https://pub.dev/packages/meta). Some commonly used annotations the package provides include:

[`@visibleForTesting`](https://pub.dev/documentation/meta/latest/meta/visibleForTesting-constant.html)
Marks a member of a package as only public so that the member can be accessed from the package's tests. The analyzer hides the member from autocompletion suggestions and warns if it's used from another package.

[`@awaitNotRequired`](https://pub.dev/documentation/meta/latest/meta/awaitNotRequired-constant.html)
Marks variables that have a `Future` type or functions that return a `Future` as not requiring the caller to await the `Future`. This stops the analyzer from warning callers that don't await the `Future` due to the [`discarded_futures`](https://dart.dev/tools/linter-rules/discarded_futures) or [`unawaited_futures`](https://dart.dev/tools/linter-rules/unawaited_futures) lints.

To learn more about these and the other annotations the package provides, what they indicate, what functionality they enable, and how to use them, check out the [`package:meta/meta.dart` API docs](https://pub.dev/documentation/meta/latest/meta/meta-library.html).

Custom annotations
------------------

[#](https://dart.dev/language/metadata#custom-annotations)

You can define your own metadata annotations. Here's an example of defining a `@Todo` annotation that takes two arguments:

dart

```
class Todo {
  final String who;
  final String what;
​
  const Todo(this.who, this.what);
}
```

And here's an example of using that `@Todo` annotation:

dart

```
@Todo('Dash', 'Implement this function')
void doSomething() {
  print('Do something');
}
```

### Specifying supported targets

[#](https://dart.dev/language/metadata#specifying-supported-targets)

To indicate the type of language constructs that should be annotated with your annotation, use the [`@Target`](https://pub.dev/documentation/meta/latest/meta_meta/Target-class.html) annotation from [`package:meta`](https://pub.dev/packages/meta).

For example, if you wanted the earlier `@Todo` annotation to only be allowed on functions and methods, you'd add the following annotation:

dart

```
import 'package:meta/meta_meta.dart';
​
@Target({TargetKind.function, TargetKind.method})
class Todo {
  // ···
}
```

With this configuration, the analyzer will warn if `Todo` is used as an annotation on any declaration besides a top-level function or method.