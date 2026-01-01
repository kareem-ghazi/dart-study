# Assignments: Concurrency in Dart

## Assignment 1: The Event Loop Prediction
**Objective:** Understand execution order with Futures.
(فهم ترتيب التنفيذ مع Futures.)

**Instructions:**
1.  Write a `main` function.
2.  Print "Start".
3.  Use `Future(() => print('Future 1'))`.
4.  Use `Future.microtask(() => print('Microtask 1'))`.
5.  Print "End".
6.  Run the code and observe the order. Explain why (in comments).

**Expected Output:**
```
Start
End
Microtask 1
Future 1
```

## Assignment 2: The Async Waiter
**Objective:** Practice `async` and `await`.
(ممارسة `async` و `await`.)

**Instructions:**
1.  Create a function `orderFood(String order)` that returns a `Future<String>`.
2.  Inside, delay for 2 seconds (`Future.delayed`), then return "Order is ready: $order".
3.  In `main`, print "Ordering...".
4.  `await` the `orderFood` function for "Pizza".
5.  Print the result.

**Expected Output:**
```
Ordering...
(2 seconds delay)
Order is ready: Pizza
```

## Assignment 3: Stream of Numbers
**Objective:** Work with `Stream` and `async*`.
(العمل مع `Stream` و `async*`.)

**Instructions:**
1.  Create a function `countDown(int n)` that returns a `Stream<int>`.
2.  Use `async*` and a loop to `yield` numbers from n down to 1.
3.  Add a 1-second delay between each yield.
4.  In `main`, use `await for` to listen to the stream and print each number.
5.  Print "Liftoff!" after the loop.

**Expected Output:**
```
3
2
1
Liftoff!
```

## Assignment 4: Heavy Lifting (Isolates)
**Objective:** Use `Isolate.run` for CPU-intensive tasks.
(استخدام `Isolate.run` للمهام الكثيفة على المعالج.)

**Instructions:**
1.  Create a function `heavyCalculation(int n)` that sums numbers from 1 to `n` (use a large number like 1,000,000,000).
2.  In `main`, print "Starting calculation...".
3.  Use `Isolate.run` to run `heavyCalculation`.
4.  `await` the result and print it.
5.  Print "Done".

**Expected Output:**
```
Starting calculation...
Result: 500000000500000000
Done
```

## Assignment 5: The Worker Spawner (Expert)
**Objective:** Use `Isolate.spawn` and ports for communication.
(استخدام `Isolate.spawn` والمنافذ للاتصال.)

**Instructions:**
1.  Create a function `worker(SendPort sendPort)`.
2.  Inside `worker`, create a `ReceivePort` to listen for messages from main.
3.  Send the `ReceivePort.sendPort` back to main via the passed `sendPort`.
4.  In `main`, create a `ReceivePort` and spawn the worker.
5.  Wait to receive the worker's port.
6.  Send a message "Hello" to the worker.
7.  The worker should print "Worker received: Hello" and exit.

**Expected Output:**
```
Worker received: Hello
```

---

## Solutions

```dart
import 'dart:async';
import 'dart:isolate';

// Assignment 1
void assignment1() {
  print('Start');
  Future(() => print('Future 1')); // Event queue
  Future.microtask(() => print('Microtask 1')); // Microtask queue (high priority)
  print('End');
}

// Assignment 2
Future<String> orderFood(String order) async {
  await Future.delayed(Duration(seconds: 2));
  return 'Order is ready: $order';
}

// Assignment 3
Stream<int> countDown(int n) async* {
  for (int i = n; i >= 1; i--) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

// Assignment 4
int heavyCalculation(int n) {
  int sum = 0;
  for (int i = 1; i <= n; i++) {
    sum += i;
  }
  return sum;
}

// Assignment 5
void worker(SendPort mainSendPort) {
  final workerReceivePort = ReceivePort();
  // Send our listening port to main
  mainSendPort.send(workerReceivePort.sendPort);

  workerReceivePort.listen((message) {
    print('Worker received: $message');
    if (message == 'Hello') {
      workerReceivePort.close();
    }
  });
}

void main() async {
  // Uncomment one assignment at a time to test

  // --- Assignment 1 ---
  // assignment1();
  // await Future.delayed(Duration(seconds: 1)); // Wait for queues to empty

  // --- Assignment 2 ---
  // print('Ordering...');
  // print(await orderFood('Pizza'));

  // --- Assignment 3 ---
  // await for (final num in countDown(3)) {
  //   print(num);
  // }
  // print('Liftoff!');

  // --- Assignment 4 ---
  // print('Starting calculation...');
  // // 1 billion loop takes time, but won't block main thread UI if valid app
  // final result = await Isolate.run(() => heavyCalculation(1000000000));
  // print('Result: $result');
  // print('Done');

  // --- Assignment 5 ---
  final mainReceivePort = ReceivePort();
  await Isolate.spawn(worker, mainReceivePort.sendPort);

  final workerSendPort = await mainReceivePort.first as SendPort;
  workerSendPort.send('Hello');
}
```
