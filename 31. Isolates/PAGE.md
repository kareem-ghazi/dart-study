# Isolates

You should use isolates whenever your application is handling computations that are large enough to temporarily block other computations. The most common example is in Flutter applications, when you need to perform large computations that might otherwise cause the UI to become unresponsive.

There aren't any rules about when you *must* use isolates, but here are some more situations where they can be useful:

*   Parsing and decoding exceptionally large JSON blobs.
*   Processing and compressing photos, audio and video.
*   Converting audio and video files.
*   Performing complex searching and filtering on large lists or within file systems.
*   Performing I/O, such as communicating with a database.
*   Handling a large volume of network requests.

## Implementing a simple worker isolate

These examples implement a main isolate that spawns a simple worker isolate. `Isolate.run()` simplifies the steps behind setting up and managing worker isolates:

1.  Spawns (starts and creates) an isolate.
2.  Runs a function on the spawned isolate.
3.  Captures the result.
4.  Returns the result to the main isolate.
5.  Terminates the isolate once work is complete.
6.  Checks, captures, and throws exceptions and errors back to the main isolate.

### Running an existing method in a new isolate

Call `run()` to spawn a new isolate, directly in the main isolate while `main()` waits for the result:

```dart
const String filename = 'with_keys.json';

void main() async {
  // Read some data.
  final jsonData = await Isolate.run(_readAndParseJson);

  // Use that data.
  print('Number of JSON keys: ${jsonData.length}');
}

Future<Map<String, dynamic>> _readAndParseJson() async {
  final fileData = await File(filename).readAsString();
  final jsonData = jsonDecode(fileData) as Map<String, dynamic>;
  return jsonData;
}
```

The worker isolate *transfers* the memory holding the result to the main isolate. It *does not copy* the data (for supported types).

### Sending closures with isolates

You can also create a simple worker isolate with `run()` using a function literal, or closure.

```dart
const String filename = 'with_keys.json';

void main() async {
  final jsonData = await Isolate.run(() async {
    final fileData = await File(filename).readAsString();
    final jsonData = jsonDecode(fileData) as Map<String, dynamic>;
    return jsonData;
  });

  print('Number of JSON keys: ${jsonData.length}');
}
```

## Sending multiple messages between isolates with ports

Short-lived isolates (`Isolate.run`) are convenient, but require performance overhead to spawn. If your code relies on repeatedly running the same computation, you might improve performance by creating long-lived isolates.

To do this, use the low-level isolate APIs:
*   `Isolate.spawn()` and `Isolate.exit()`
*   `ReceivePort` and `SendPort`
*   `SendPort.send()` method

### `ReceivePort` and `SendPort`

Setting up long-lived communication between isolates requires two classes: `ReceivePort` and `SendPort`.

A `ReceivePort` is an object that handles messages that are sent from other isolates. Those messages are sent via a `SendPort`.

1.  Create a `ReceivePort` in the main isolate. The `SendPort` is created automatically as a property on the `ReceivePort`.
2.  Spawn the worker isolate with `Isolate.spawn()`.
3.  Pass a reference to `ReceivePort.sendPort` as the first message to the worker isolate.
4.  Create another new `ReceivePort` in the worker isolate.
5.  Pass a reference to the worker isolate's `ReceivePort.sendPort` as the first message *back* to the main isolate.

### Basic ports example

**Step 1: Spawn a worker isolate**

```dart
Future<void> spawn() async {
  final receivePort = ReceivePort();
  receivePort.listen(_handleResponsesFromIsolate);
  await Isolate.spawn(_startRemoteIsolate, receivePort.sendPort);
}
```

**Step 2: Execute code on the worker isolate**

```dart
static void _startRemoteIsolate(SendPort port) {
  final receivePort = ReceivePort();
  port.send(receivePort.sendPort);

  receivePort.listen((dynamic message) async {
    if (message is String) {
      final transformed = jsonDecode(message);
      port.send(transformed);
    }
  });
}
```

**Step 3: Handle messages on the main isolate**

```dart
void _handleResponsesFromIsolate(dynamic message) {
  if (message is SendPort) {
    _sendPort = message;
    _isolateReady.complete();
  } else if (message is Map<String, dynamic>) {
    print(message);
  }
}
```

For robust implementation (error handling, closing ports, request matching), you need to implement additional logic to manage `Completer`s and message IDs.
