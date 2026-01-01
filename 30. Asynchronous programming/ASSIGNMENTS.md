# Assignments: Asynchronous Programming

## Assignment 1: The Late Comer
**Objective:** Create a basic async function.
(إنشاء دالة غير متزامنة أساسية.)

**Instructions:**
1.  Create a function `fetchUsername()` that returns `Future<String>`.
2.  Delay for 2 seconds.
3.  Return "DartUser".
4.  In `main`, print "Fetching...".
5.  Call and `await` the function, then print the result.

**Expected Output:**
```
Fetching...
(2 second delay)
DartUser
```

## Assignment 2: The Broken Link
**Objective:** Handle async errors using `try-catch`.
(معالجة الأخطاء غير المتزامنة باستخدام `try-catch`.)

**Instructions:**
1.  Create a function `fetchData(bool success)` that returns `Future<String>`.
2.  Delay for 1 second.
3.  If `success` is false, throw an exception "Network Error".
4.  Otherwise return "Data Found".
5.  In `main`, call `fetchData(false)` inside a `try-catch` block and print the error.

**Expected Output:**
```
Error: Exception: Network Error
```

## Assignment 3: Chain Reaction
**Objective:** Execute multiple async tasks sequentially.
(تنفيذ مهام متعددة غير متزامنة بالتسلسل.)

**Instructions:**
1.  Create three functions: `step1()`, `step2()`, `step3()`.
2.  Each should delay 1 second and print "Step X done".
3.  Create a function `runProcess()` that awaits them in order (1, then 2, then 3).
4.  Call `runProcess` in `main`.

**Expected Output:**
```
Step 1 done
Step 2 done
Step 3 done
```

## Assignment 4: Fast Food Stream
**Objective:** Process a stream of data using `await for`.
(معالجة تيار من البيانات باستخدام `await for`.)

**Instructions:**
1.  Create a function `getOrders()` that returns `Stream<String>`.
2.  Yield "Burger", "Fries", "Soda" with a 1-second delay between each.
3.  In `main`, use `await for` to print "Serving: [item]" for each order.

**Expected Output:**
```
Serving: Burger
Serving: Fries
Serving: Soda
```

## Assignment 5: The Status Checker (Expert)
**Objective:** Wait for multiple futures simultaneously (Concept extension).
(انتظار عدة مستقبليات في وقت واحد.)

**Instructions:**
1.  Create a function `checkServer(String name)` that delays for a random time (1-3 seconds) and returns "$name: Online".
2.  In `main`, start checking "Server A", "Server B", and "Server C" *at the same time* (store the futures in variables, don't await immediately).
3.  Then await all of them (Hint: You can await them one by one, or use `Future.wait` if you know it, but awaiting variables sequentially after starting them is also "concurrent").
4.  Print all results.

**Expected Output:**
```
(After max 3 seconds)
Server A: Online
Server B: Online
Server C: Online
```

---

## Solutions

```dart
import 'dart:async';
import 'dart:math';

// Assignment 1
Future<String> fetchUsername() async {
  await Future.delayed(Duration(seconds: 2));
  return 'DartUser';
}

// Assignment 2
Future<String> fetchData(bool success) async {
  await Future.delayed(Duration(seconds: 1));
  if (!success) throw Exception('Network Error');
  return 'Data Found';
}

// Assignment 3
Future<void> step1() async {
  await Future.delayed(Duration(seconds: 1));
  print('Step 1 done');
}
Future<void> step2() async {
  await Future.delayed(Duration(seconds: 1));
  print('Step 2 done');
}
Future<void> step3() async {
  await Future.delayed(Duration(seconds: 1));
  print('Step 3 done');
}

Future<void> runProcess() async {
  await step1();
  await step2();
  await step3();
}

// Assignment 4
Stream<String> getOrders() async* {
  await Future.delayed(Duration(seconds: 1));
  yield 'Burger';
  await Future.delayed(Duration(seconds: 1));
  yield 'Fries';
  await Future.delayed(Duration(seconds: 1));
  yield 'Soda';
}

// Assignment 5
Future<String> checkServer(String name) async {
  var delay = Random().nextInt(3) + 1;
  await Future.delayed(Duration(seconds: delay));
  return '$name: Online';
}

void main() async {
  // 1.
  print('Fetching...');
  print(await fetchUsername());

  // 2.
  try {
    await fetchData(false);
  } catch (e) {
    print('Error: $e');
  }

  // 3.
  await runProcess();

  // 4.
  await for (var item in getOrders()) {
    print('Serving: $item');
  }

  // 5.
  // Start all at once
  var futureA = checkServer('Server A');
  var futureB = checkServer('Server B');
  var futureC = checkServer('Server C');

  // Wait for all
  print(await futureA);
  print(await futureB);
  print(await futureC);
}
```
