Asynchronous programming
========================

Information on writing asynchronous code in Dart.

more_vert

*   copy Copy link
*   [docs View source](https://github.com/dart-lang/site-www/blob/main/src/content/language/async.md)
*   [bug_report Report issue](https://github.com/dart-lang/site-www/issues/new?template=1_page_issue.yml&page-url=https://dart.dev/language/async&page-source=https://github.com/dart-lang/site-www/blob/main/src/content/language/async.md)

Dart libraries are full of functions that return [`Future`](https://api.dart.dev/dart-async/Future-class.html) or [`Stream`](https://api.dart.dev/dart-async/Stream-class.html) objects. These functions are _asynchronous_: they return after setting up a possibly time-consuming operation (such as I/O), without waiting for that operation to complete.

The `async` and `await` keywords support asynchronous programming, letting you write asynchronous code that looks similar to synchronous code.

Handling Futures
----------------

[#](https://dart.dev/language/async#handling-futures)

When you need the result of a completed Future, you have two options:

*    Use `async` and `await`, as described here and in the [asynchronous programming tutorial](https://dart.dev/libraries/async/async-await). 
*    Use the Future API, as described in the [`dart:async` documentation](https://dart.dev/libraries/dart-async#future). 

Code that uses `async` and `await` is asynchronous, but it looks a lot like synchronous code. For example, here's some code that uses `await` to wait for the result of an asynchronous function:

dart
```
await lookUpVersion();
```
content_copy

To use `await`, code must be in an `async` function—a function marked as `async`:

dart
```
Future<void> checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```
content_copy

info Note

Although an `async` function might perform time-consuming operations, it doesn't wait for those operations. Instead, the `async` function executes only until it encounters its first `await` expression. Then it returns a `Future` object, resuming execution only after the `await` expression completes.

Use `try`, `catch`, and `finally` to handle errors and cleanup in code that uses `await`:

dart
```
try {
  version = await lookUpVersion();
} catch (e) {
  // React to inability to look up the version
}
```
content_copy

You can use `await` multiple times in an `async` function. For example, the following code waits three times for the results of functions:

dart
```
var entrypoint = await findEntryPoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```
content_copy

In `await expression`, the value of `expression` is usually a Future; if it isn't, then the value is automatically wrapped in a Future. This Future object indicates a promise to return an object. The value of `await expression` is that returned object. The await expression makes execution pause until that object is available.

**If you get a compile-time error when using `await`, make sure `await` is in an `async` function.** For example, to use `await` in your app's `main()` function, the body of `main()` must be marked as `async`:

dart
```
void main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```
content_copy

info Note

The preceding example uses an `async` function (`checkVersion()`) without waiting for a result—a practice that can cause problems if the code assumes that the function has finished executing. To avoid this problem, use the [unawaited_futures linter rule](https://dart.dev/tools/linter-rules/unawaited_futures).

For an interactive introduction to using futures, `async`, and `await`, see the [asynchronous programming tutorial](https://dart.dev/libraries/async/async-await).

Declaring async functions
-------------------------

[#](https://dart.dev/language/async#declaring-async-functions)

An `async` function is a function whose body is marked with the `async` modifier.

Adding the `async` keyword to a function makes it return a Future. For example, consider this synchronous function, which returns a String:

dart
```
String lookUpVersion() => '1.0.0';
```
content_copy

If you change it to be an `async` function—for example, because a future implementation will be time consuming—the returned value is a Future:

dart
```
Future<String> lookUpVersion() async => '1.0.0';
```
content_copy

Note that the function's body doesn't need to use the Future API. Dart creates the Future object if necessary. If your function doesn't return a useful value, make its return type `Future<void>`.

For an interactive introduction to using futures, `async`, and `await`, see the [asynchronous programming tutorial](https://dart.dev/libraries/async/async-await).

Handling Streams
----------------

[#](https://dart.dev/language/async#handling-streams)

When you need to get values from a Stream, you have two options:

*   Use `async` and an _asynchronous for loop_ (`await for`).
*    Use the Stream API, as described in the [`dart:async` documentation](https://dart.dev/libraries/dart-async#stream). 

info Note

Before using `await for`, be sure that it makes the code clearer and that you really do want to wait for all of the stream's results. For example, you usually should **not** use `await for` for UI event listeners, because UI frameworks send endless streams of events.

An asynchronous for loop has the following form:

dart
```
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```
content_copy

The value of `expression` must have type Stream. Execution proceeds as follows:

1.   Wait until the stream emits a value.
2.    Execute the body of the for loop, with the variable set to that emitted value. 
3.   Repeat 1 and 2 until the stream is closed.

To stop listening to the stream, you can use a `break` or `return` statement, which breaks out of the for loop and unsubscribes from the stream.

**If you get a compile-time error when implementing an asynchronous for loop, make sure the `await for` is in an `async` function.** For example, to use an asynchronous for loop in your app's `main()` function, the body of `main()` must be marked as `async`:

dart
```
void main() async {
  // ...
  await for (final request in requestServer) {
    handleRequest(request);
  }
  // ...
}
```
content_copy

For more information about Dart's asynchronous programming support, check out the [`dart:async`](https://dart.dev/libraries/dart-async) library documentation.