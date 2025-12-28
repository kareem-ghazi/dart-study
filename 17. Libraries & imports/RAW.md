Libraries & imports
===================

Guidance on importing and implementing libraries.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/libraries.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/libraries&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/libraries.md)

The `import` and `library` directives can help you create a modular and shareable code base. Libraries not only provide APIs, but are a unit of privacy: identifiers that start with an underscore (`_`) are visible only inside the library. _Every Dart file (plus its parts) is a [library](https://dart.dev/resources/glossary#library)Library A single compilation unit in Dart, made up of a primary Dart file and its parts. [Learn more](https://dart.dev/resources/glossary#library "Learn more about 'Library' and find related resources.")_, even if it doesn't use a [`library`](https://dart.dev/language/libraries#library-directive) directive.

Libraries can be distributed using [packages](https://dart.dev/tools/pub/packages).

Dart uses underscores instead of access modifier keywords like `public`, `protected`, or `private`. While access modifier keywords from other languages provide more fine-grained control, Dart's use of underscores and library-based privacy provides a straightforward configuration mechanism, helps enable an efficient implementation of [dynamic access](https://dart.dev/effective-dart/design#avoid-using-dynamic-unless-you-want-to-disable-static-checking), and improves tree shaking (dead code elimination).

Using libraries
---------------

[#](https://dart.dev/language/libraries#using-libraries)

Use `import` to specify how a namespace from one library is used in the scope of another library.

For example, Dart web apps generally use the [`dart:js_interop`](https://api.dart.dev/dart-js_interop/dart-js_interop-library.html) library, which they can import like this:

dart
```
import 'dart:js_interop';
```
content_copy

The only required argument to `import` is a URI specifying the library. For built-in libraries, the URI has the special `dart:` scheme. For other libraries, you can use a file system path or the `package:` scheme. The `package:` scheme specifies libraries provided by a package manager such as the pub tool. For example:

dart
```
import 'package:test/test.dart';
```
content_copy

info Note

_URI_ stands for uniform resource identifier. _URLs_ (uniform resource locators) are a common kind of URI.

### Specifying a library prefix

[#](https://dart.dev/language/libraries#specifying-a-library-prefix)

If you import two libraries that have conflicting identifiers, then you can specify a prefix for one or both libraries. For example, if library1 and library2 both have an Element class, then you might have code like this:

dart
```
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;
​
// Uses Element from lib1.
Element element1 = Element();
​
// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```
content_copy

Import prefixes with the [wildcard](https://dart.dev/language/variables#wildcard-variables) name `_` are non-binding, but will provide access to the non-private extensions in that library.

### Importing only part of a library

[#](https://dart.dev/language/libraries#importing-only-part-of-a-library)

If you want to use only part of a library, you can selectively import the library. For example:

dart
```
// Import only foo.
import 'package:lib1/lib1.dart' show foo;
​
// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
```
content_copy

#### Lazily loading a library

[#](https://dart.dev/language/libraries#lazily-loading-a-library)

_Deferred loading_ (also called _lazy loading_) allows a web app to load a library on demand, if and when the library is needed. Use deferred loading when you want to meet one or more of the following needs.

*   Reduce a web app's initial startup time.
*    Perform A/B testing—trying out alternative implementations of an algorithm, for example. 
*   Load rarely used functionality, such as optional screens and dialogs.

That doesn't mean Dart loads all the deferred components at start time. The web app can download deferred components via the web when needed.

The `dart` tool doesn't support deferred loading for targets other than web. If you're building a Flutter app, consult its implementation of deferred loading in the Flutter guide on [deferred components](https://docs.flutter.dev/perf/deferred-components).

To lazily load a library, first import it using `deferred as`.

dart
```
import 'package:greetings/hello.dart' deferred as hello;
```
content_copy

When you need the library, invoke `loadLibrary()` using the library's identifier.

dart
```
Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```
content_copy

In the preceding code, the `await` keyword pauses execution until the library is loaded. For more information about `async` and `await`, check out [asynchronous programming](https://dart.dev/language/async).

You can invoke `loadLibrary()` multiple times on a library without problems. The library is loaded only once.

Keep in mind the following when you use deferred loading:

*    A deferred library's constants aren't constants in the importing file. Remember, these constants don't exist until the deferred library is loaded. 
*    You can't use types from a deferred library in the importing file. Instead, consider moving interface types to a library imported by both the deferred library and the importing file. 
*    Dart implicitly inserts `loadLibrary()` into the namespace that you define using `deferred as namespace`. The `loadLibrary()` function returns a [`Future`](https://dart.dev/libraries/dart-async#future). 

### The `library` directive

[#](https://dart.dev/language/libraries#library-directive)

To specify library-level [doc comments](https://dart.dev/effective-dart/documentation#consider-writing-a-library-level-doc-comment) or [metadata annotations](https://dart.dev/language/metadata), attach them to a `library` declaration at the start of the file.

dart
```
/// A really great test library.
@TestOn('browser')
library;
```
content_copy

Implementing libraries
----------------------

[#](https://dart.dev/language/libraries#implementing-libraries)

See [Create Packages](https://dart.dev/tools/pub/create-packages) for advice on how to implement a package, including:

*   How to organize library source code.
*   How to use the `export` directive.
*   When to use the `part` directive.
*    How to use conditional imports and exports to implement a library that supports multiple platforms. 
