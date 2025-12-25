Error handling
==============

Learn about handling errors and exceptions in Dart.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/error-handling.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/error-handling&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/error-handling.md)

Exceptions
----------

[#](https://dart.dev/language/error-handling#exceptions)

Your Dart code can throw and catch exceptions. Exceptions are errors indicating that something unexpected happened. If the exception isn't caught, the [isolate](https://dart.dev/language/concurrency#isolates) that raised the exception is suspended, and typically the isolate and its program are terminated.

In contrast to Java, all of Dart's exceptions are unchecked exceptions. Methods don't declare which exceptions they might throw, and you aren't required to catch any exceptions.

Dart provides [`Exception`](https://api.dart.dev/dart-core/Exception-class.html) and [`Error`](https://api.dart.dev/dart-core/Error-class.html) types, as well as numerous predefined subtypes. You can, of course, define your own exceptions. However, Dart programs can throw any non-null object—not just Exception and Error objects—as an exception.

### Throw

[#](https://dart.dev/language/error-handling#throw)

Here's an example of throwing, or _raising_, an exception:

dart
```
throw FormatException('Expected at least 1 section');
```
content_copy

You can also throw arbitrary objects:

dart
```
throw 'Out of llamas!';
```
content_copy

info Note

Production-quality code usually throws types that implement [`Error`](https://api.dart.dev/dart-core/Error-class.html) or [`Exception`](https://api.dart.dev/dart-core/Exception-class.html).

Because throwing an exception is an expression, you can throw exceptions in => statements, as well as anywhere else that allows expressions:

dart
```
void distanceTo(Point other) => throw UnimplementedError();
```
content_copy

### Catch

[#](https://dart.dev/language/error-handling#catch)

Catching, or capturing, an exception stops the exception from propagating (unless you rethrow the exception). Catching an exception gives you a chance to handle it:

dart
```
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```
content_copy

To handle code that can throw more than one type of exception, you can specify multiple catch clauses. The first catch clause that matches the thrown object's type handles the exception. If the catch clause does not specify a type, that clause can handle any type of thrown object:

dart
```
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}
```
content_copy

As the preceding code shows, you can use either `on` or `catch` or both. Use `on` when you need to specify the exception type. Use `catch` when your exception handler needs the exception object.

You can specify one or two parameters to `catch()`. The first is the exception that was thrown, and the second is the stack trace (a [`StackTrace`](https://api.dart.dev/dart-core/StackTrace-class.html) object).

dart
```
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```
content_copy

To partially handle an exception, while allowing it to propagate, use the `rethrow` keyword.

dart
```
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow; // Allow callers to see the exception.
  }
}
​
void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```
content_copy

### Finally

[#](https://dart.dev/language/error-handling#finally)

To ensure that some code runs whether or not an exception is thrown, use a `finally` clause. If no `catch` clause matches the exception, the exception is propagated after the `finally` clause runs:

dart
```
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}
```
content_copy

The `finally` clause runs after any matching `catch` clauses:

dart
```
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```
content_copy

To learn more, check out the [core library exception docs](https://dart.dev/libraries/dart-core#exceptions).

Assert
------

[#](https://dart.dev/language/error-handling#assert)

During development, use an assert statement— `assert(<condition>, <optionalMessage>);` —to disrupt normal execution if a boolean condition is false.

dart
```
// Make sure the variable has a non-null value.
assert(text != null);
​
// Make sure the value is less than 100.
assert(number < 100);
​
// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```
content_copy

To attach a message to an assertion, add a string as the second argument to `assert` (optionally with a [trailing comma](https://dart.dev/language/collections#trailing-comma)):

dart
```
assert(
  urlString.startsWith('https'),
  'URL ($urlString) should start with "https".',
);
```
content_copy

The first argument to `assert` can be any expression that resolves to a boolean value. If the expression's value is true, the assertion succeeds and execution continues. If it's false, the assertion fails and an exception (an [`AssertionError`](https://api.dart.dev/dart-core/AssertionError-class.html)) is thrown.

When exactly do assertions work? That depends on the tools and framework you're using:

*    Flutter enables assertions in [debug mode.](https://docs.flutter.dev/testing/debugging#debug-mode-assertions)
*    Development-only tools such as [`webdev serve`](https://dart.dev/tools/webdev#serve) typically enable assertions by default. 
*    Some tools, such as [`dart run`](https://dart.dev/tools/dart-run) and [`dart compile js`](https://dart.dev/tools/dart-compile#js) support assertions through a command-line flag: `--enable-asserts`. 

In production code, assertions are ignored, and the arguments to `assert` aren't evaluated.