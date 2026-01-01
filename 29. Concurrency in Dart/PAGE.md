# Concurrency in Dart

Concurrent programming in Dart refers to both asynchronous APIs, like `Future` and `Stream`, and *isolates*, which allow you to move processes to separate cores.

All Dart code runs in isolates, starting in the default main isolate, and optionally expanding to whatever subsequent isolates you explicitly create. When you spawn a new isolate, it has its own isolated memory, and its own event loop. The event loop is what makes asynchronous and concurrent programming possible in Dart.

## Event Loop

Dart’s runtime model is based on an event loop. The event loop is responsible for executing your program's code, collecting and processing events, and more.

As your application runs, all events are added to a queue, called the *event queue*. Events can be anything from requests to repaint the UI, to user taps and keystrokes, to I/O from the disk. Because your app can’t predict what order events will happen, the event loop processes events in the order they're queued, one at a time.

The way the event loop functions resembles this code:

```dart
while (eventQueue.waitForEvent()) {
  eventQueue.processNextEvent();
}
```

This example event loop is synchronous and runs on a single thread. However, most Dart applications need to do more than one thing at a time. For example, a client application might need to execute an HTTP request, while also listening for a user to tap a button. To handle this, Dart offers many async APIs, like Futures, Streams, and async-await. These APIs are built around this event loop.

## Asynchronous programming

This section summarizes the different types and syntaxes of asynchronous programming in Dart.

### Futures

A `Future` represents the result of an asynchronous operation that will eventually complete with a value or an error.

```dart
Future<String> _readFileAsync(String filename) {
  final file = File(filename);

  // .readAsString() returns a Future.
  // .then() registers a callback to be executed when `readAsString` resolves.
  return file.readAsString().then((contents) {
    return contents.trim();
  });
}
```

### The async-await syntax

The `async` and `await` keywords provide a declarative way to define asynchronous functions and use their results.

```dart
const String filename = 'with_keys.json';

void main() async {
  // Read some data.
  final fileData = await _readFileAsync();
  final jsonData = jsonDecode(fileData);

  // Use that data.
  print('Number of JSON keys: ${jsonData.length}');
}

Future<String> _readFileAsync() async {
  final file = File(filename);
  final contents = await file.readAsString();
  return contents.trim();
}
```

The `main()` function uses the `await` keyword in front of `_readFileAsync()` to let other Dart code (such as event handlers) use the CPU while native code (file I/O) executes. Using `await` also has the effect of converting the `Future<String>` returned by `_readFileAsync()` into a `String`.

### Streams

Dart also supports asynchronous code in the form of streams. Streams provide values in the future and repeatedly over time. A promise to provide a series of `int` values over time has the type `Stream<int>`.

In the following example, the stream created with `Stream.periodic` repeatedly emits a new `int` value every second.

```dart
Stream<int> stream = Stream.periodic(const Duration(seconds: 1), (i) => i * i);
```

#### await-for and yield

Await-for is a type of for loop that executes each subsequent iteration of the loop as new values are provided. It’s used to “loop over” streams. The `yield` keyword is used rather than `return` in functions that return streams of values.

```dart
Stream<int> sumStream(Stream<int> stream) async* {
  var sum = 0;
  await for (final value in stream) {
    yield sum += value;
  }
}
```

## Isolates

Dart supports concurrency via isolates, in addition to asynchronous APIs. Instead of threads, all Dart code runs inside isolates. Using isolates, your Dart code can perform multiple independent tasks at once, using additional processor cores if they're available. Isolates are like threads or processes, but each isolate has its own memory and a single thread running an event loop.

Each isolate has its own global fields, ensuring that none of the state in an isolate is accessible from any other isolate. Isolates can only communicate to each other via message passing. No shared state between isolates means concurrency complexities like mutexes or locks and data races won't occur in Dart.

### The main isolate

In most cases, you don't need to think about isolates at all. Dart programs run in the main isolate by default. It’s the thread where a program starts to run and execute.

### Background workers

If your app's UI becomes unresponsive due to a time-consuming computation—parsing a large JSON file, for example—consider offloading that computation to a worker isolate, often called a *background worker.*

## Using isolates

There are two ways to work with isolates in Dart, depending on the use-case:

*   Use `Isolate.run()` to perform a single computation on a separate thread.
*   Use `Isolate.spawn()` to create an isolate that will handle multiple messages over time, or a background worker.

In most cases, `Isolate.run` is the recommended API to run processes in the background.

### `Isolate.run()`

The static `Isolate.run()` method requires one argument: a callback that will be run on the newly spawned isolate.

```dart
int slowFib(int n) => n <= 1 ? 1 : slowFib(n - 1) + slowFib(n - 2);

// Compute without blocking current isolate.
void fib40() async {
  var result = await Isolate.run(() => slowFib(40));
  print('Fib(40) = $result');
}
```

## Limitations of isolates

### Isolates aren't threads

Each isolate has its own state, ensuring that none of the state in an isolate is accessible from any other isolate. Therefore, isolates are limited by their access to their own memory.

For example, if you have an application with a global mutable variable, that variable will be a separate variable in your spawned isolate. If you mutate that variable in the spawned isolate, it will remain untouched in the main isolate.

### Message types

Messages sent via `SendPort` can be almost any type of Dart object, but there are a few exceptions (e.g., objects with native resources like `Socket`).

## Concurrency on the web

All Dart apps can use `async-await`, `Future`, and `Stream` for non-blocking, interleaved computations. The Dart web platform, however, does not support isolates. Dart web apps can use web workers to run scripts in background threads similar to isolates.
