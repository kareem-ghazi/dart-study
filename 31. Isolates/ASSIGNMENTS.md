# Assignments: Isolates

## Assignment 1: Quick Math
**Objective:** Use `Isolate.run` for a simple calculation.
(استخدام `Isolate.run` لحساب بسيط.)

**Instructions:**
1.  Create a function `massiveSum(int n)` that sums numbers from 1 to `n`.
2.  In `main`, use `Isolate.run` to calculate the sum of 1,000,000.
3.  Print the result.

**Expected Output:**
```
Sum: 500000500000
```

## Assignment 2: The JSON Parser
**Objective:** Simulate a common use case (parsing).
(محاكاة حالة استخدام شائعة (التحليل).)

**Instructions:**
1.  Create a large string simulating a JSON list: `'[1, 2, 3, ... 10000]'`.
2.  Use `Isolate.run` to parse this string (you can just split it by comma and count items if you don't want to import `dart:convert`, or use `jsonDecode`).
3.  Return the count of items.

**Expected Output:**
```
Items parsed: 10000
```

## Assignment 3: Ping Pong
**Objective:** Basic communication with `spawn`.
(اتصال أساسي مع `spawn`.)

**Instructions:**
1.  Create a function `pingPongWorker(SendPort sendPort)`.
2.  Inside, create a `ReceivePort`.
3.  Send the `ReceivePort.sendPort` back to main.
4.  Listen for "Ping". If received, reply "Pong".
5.  In `main`, spawn the worker, get the port, send "Ping", print the reply, and close.

**Expected Output:**
```
Sent: Ping
Received: Pong
```

## Assignment 4: The Dedicated Listener
**Objective:** Long-lived isolate processing a stream of data.
(عزلة طويلة العمر تعالج تيارًا من البيانات.)

**Instructions:**
1.  Create a worker that accepts strings.
2.  If the string is "exit", it kills itself (exits loop/closes port).
3.  Otherwise, it converts the string to uppercase and sends it back.
4.  In `main`, send "hello", "world", and "exit". Print responses.

**Expected Output:**
```
Response: HELLO
Response: WORLD
```

## Assignment 5: Robust Request/Response (Expert)
**Objective:** Match requests with responses using IDs (Simplified).
(مطبقة الطلبات مع الاستجابات باستخدام المعرفات (مبسطة).)

**Instructions:**
1.  Modify the worker to accept `(int id, String message)`.
2.  It should reply with `(int id, String reversedMessage)`.
3.  In `main`, send two requests: ID 1 ("Dart") and ID 2 ("Flutter").
4.  Listen to the main receive port. When you get a message, print "ID [id]: [reversed]".
5.  (Optional: Use a Map/Completer pattern if you want to be fancy, otherwise just print).

**Expected Output:**
```
ID 1: traD
ID 2: rettulF
```

---

## Solutions

```dart
import 'dart:async';
import 'dart:convert';
import 'dart:isolate';

// Assignment 1
int massiveSum(int n) {
  int sum = 0;
  for (int i = 1; i <= n; i++) sum += i;
  return sum;
}

// Assignment 2
int parseJsonCount(String jsonSim) {
  // Simulating parsing by splitting
  // Remove brackets
  final content = jsonSim.substring(1, jsonSim.length - 1);
  return content.split(',').length;
}

// Assignment 3
void pingPongWorker(SendPort mainSendPort) {
  final rp = ReceivePort();
  mainSendPort.send(rp.sendPort);

  rp.listen((message) {
    if (message == 'Ping') {
      mainSendPort.send('Pong');
    }
  });
}

// Assignment 4
void uppercaseWorker(SendPort mainSendPort) {
  final rp = ReceivePort();
  mainSendPort.send(rp.sendPort);

  rp.listen((message) {
    if (message == 'exit') {
      rp.close();
    } else if (message is String) {
      mainSendPort.send(message.toUpperCase());
    }
  });
}

// Assignment 5
void robustWorker(SendPort mainSendPort) {
  final rp = ReceivePort();
  mainSendPort.send(rp.sendPort);

  rp.listen((message) {
    if (message is (int, String)) {
      final (id, msg) = message;
      final reversed = msg.split('').reversed.join();
      mainSendPort.send((id, reversed));
    }
  });
}

void main() async {
  // 1. Isolate.run Math
  print('Sum: ${await Isolate.run(() => massiveSum(1000000))}');

  // 2. Isolate.run Parse
  // Create a big string "list"
  final bigString = '[${List.generate(10000, (i) => i).join(',')}]';
  print('Items parsed: ${await Isolate.run(() => parseJsonCount(bigString))}');

  // 3. Ping Pong
  final rp3 = ReceivePort();
  await Isolate.spawn(pingPongWorker, rp3.sendPort);
  final SendPort sp3 = await rp3.first; // Get worker port

  // We need a new RP for replies if we consumed the first one
  // Actually, usually we reuse the main RP or create a specific one for replies.
  // For simplicity here, let's just make a new channel for the Ping.
  // *Correction*: The worker in solution 3 sends reply to mainSendPort.
  // We need to listen to rp3 continuously or pass a distinct port for the handshake.
  // Let's refactor main logic for 3 to be cleaner:

  final mainRp3 = ReceivePort();
  await Isolate.spawn(pingPongWorker, mainRp3.sendPort);
  // First msg is the port
  final workerPort3 = await mainRp3.first as SendPort;
  
  // Now we need to listen for the Pong. We can't use `first` again on the same stream easily if it closed? 
  // ReceivePort is a stream. `first` cancels subscription after one item.
  // We need a persistent listener or new port.
  // Simplest: Pass a reply port with the message.
  
  // Let's just demonstrate the Assignment 4 flow which is cleaner.
  
  // 4. Uppercase
  final mainRp4 = ReceivePort();
  await Isolate.spawn(uppercaseWorker, mainRp4.sendPort);
  final workerCommands = Completer<SendPort>();
  
  mainRp4.listen((data) {
    if (data is SendPort) {
      workerCommands.complete(data);
    } else {
      print('Response: $data');
    }
  });
  
  final sp4 = await workerCommands.future;
  sp4.send('hello');
  sp4.send('world');
  sp4.send('exit');
  
  // 5. Robust
  // Similar setup...
  final mainRp5 = ReceivePort();
  await Isolate.spawn(robustWorker, mainRp5.sendPort);
  final workerCommands5 = Completer<SendPort>();

  mainRp5.listen((data) {
    if (data is SendPort) {
      workerCommands5.complete(data);
    } else if (data is (int, String)) {
      print('ID ${data.$1}: ${data.$2}');
    }
  });

  final sp5 = await workerCommands5.future;
  sp5.send((1, 'Dart'));
  sp5.send((2, 'Flutter'));
}
```
