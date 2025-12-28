# Assignments: Branches

Master decision-making in Dart using `if`, `switch` statements, and `switch` expressions.

## Assignment 1: Grade Calculator
**Objective:** Use `if`, `else if`, and `else` logic.
*(الهدف: استخدام منطق `if` و `else if` و `else`.)*

**Instructions:**
1.  Write a function `calculateGrade(int score)`.
2.  Return a String grade based on the score:
    *   90 or above: "A"
    *   80 to 89: "B"
    *   70 to 79: "C"
    *   60 to 69: "D"
    *   Below 60: "F"
3.  Test with scores: 95, 82, 40.

**Expected Output:**
```
95 is A
82 is B
40 is F
```

---

## Assignment 2: Command Handler
**Objective:** Use a `switch` **statement** to execute actions.
*(الهدف: استخدام جملة `switch` لتنفيذ إجراءات.)*

**Instructions:**
1.  Create a variable `command` (String).
2.  Use a `switch` statement to handle:
    *   'START': Print "System starting..."
    *   'STOP': Print "System stopping..."
    *   'PAUSE': Print "System paused."
    *   Any other string: Print "Unknown command."
3.  Test it with 'START' and 'RESET'.

**Expected Output:**
```
System starting...
Unknown command.
```

---

## Assignment 3: Payment Processor (Sealed Classes)
**Objective:** Use a `switch` **expression** with a `sealed` class hierarchy.
*(الهدف: استخدام تعبير `switch` مع هيكلية فئات `sealed`.)*

**Instructions:**
1.  Define a `sealed class Payment`.
2.  Create two subclasses: `Cash` and `CreditCard(double fee)`.
3.  Write a function `processPayment(double amount, Payment method)` that returns the final total (double).
4.  Use a `switch` expression:
    *   If `Cash`, return just the amount.
    *   If `CreditCard`, return `amount + fee`.
5.  Call the function with both types and print the result.

**Expected Output:**
```
Cash: $100.0
Credit Card: $102.5
```

---

## Assignment 4: Exhaustive Switch on Sealed Class (Advanced)

**Objective:**
Ensure all possible states are handled using `sealed` classes and exhaustiveness checking.
*(الهدف: التأكد من معالجة جميع الحالات الممكنة باستخدام الفئات المختومة والتحقق من الشمولية.)*

**Instructions:**
1. Define `sealed class AuthState {}`.
2. Define subclasses `Authenticated`, `Unauthenticated`, and `Loading`.
3. Create a function `String getMessage(AuthState state)`.
4. Return a message using a `switch` expression.
   - Note: Do NOT use a default case (`_`). Rely on Dart's compiler to force you to handle all 3 subclasses.
5. Print messages for all 3 states.

**Expected Output:**
```
User is logged in
Please log in
Loading...
```

---

## Assignment 5: State Machine Parser (Expert)

**Objective:**
Implement a state machine using `switch` expressions to handle transitions based on events.
*(الهدف: تنفيذ آلة حالة باستخدام تعبيرات `switch` لمعالجة الانتقالات بناءً على الأحداث.)*

**Instructions:**
1.  Define a sealed class `State` (Idle, Active, Error).
2.  Define a sealed class `Event` (Start, Stop, Fail).
3.  Write a function `State nextState(State current, Event event)`.
4.  Use a `switch` expression on `(current, event)` (pair) to define transitions:
    *   (Idle, Start) -> Active
    *   (Active, Stop) -> Idle
    *   (Active, Fail) -> Error
    *   (Error, Stop) -> Idle
    *   Anything else -> current (no change).
5.  Simulate a flow: Idle -> Start -> Fail -> Stop. Print state after each step.

**Expected Output:**
```
Initial: Idle
Event Start -> Active
Event Fail -> Error
Event Stop -> Idle
```

---

## Solutions

### Solution 1: Grade Calculator

```dart
String calculateGrade(int score) {
  if (score >= 90) return 'A';
  if (score >= 80) return 'B';
  if (score >= 70) return 'C';
  if (score >= 60) return 'D';
  return 'F';
}

void main() {
  var scores = [95, 82, 40];
  for (var s in scores) {
    print('$s is ${calculateGrade(s)}');
  }
}
```

### Solution 2: Command Handler

```dart
void handleCommand(String command) {
  switch (command) {
    case 'START':
      print('System starting...');
    case 'STOP':
      print('System stopping...');
    case 'PAUSE':
      print('System paused.');
    default:
      print('Unknown command.');
  }
}

void main() {
  handleCommand('START');
  handleCommand('RESET');
}
```

### Solution 3: Payment Processor

```dart
sealed class Payment {}
class Cash extends Payment {}
class CreditCard extends Payment {
  final double fee;
  CreditCard(this.fee);
}

double processPayment(double amount, Payment method) {
  return switch (method) {
    Cash() => amount,
    CreditCard(fee: var f) => amount + f,
  };
}

void main() {
  print('Cash: \$${processPayment(100, Cash())}');
  print('Credit Card: \$${processPayment(100, CreditCard(2.5))}');
}
```

### Solution 4: Exhaustive Switch on Sealed Class

```dart
sealed class AuthState {}
class Authenticated extends AuthState {}
class Unauthenticated extends AuthState {}
class Loading extends AuthState {}

String getMessage(AuthState state) => switch (state) {
  Authenticated() => 'User is logged in',
  Unauthenticated() => 'Please log in',
  Loading() => 'Loading...',
};

void main() {
  print(getMessage(Authenticated()));
  print(getMessage(Unauthenticated()));
  print(getMessage(Loading()));
}
```

### Solution 5: State Machine Parser

```dart
sealed class State {
  @override
  String toString() => runtimeType.toString();
}
class Idle extends State {}
class Active extends State {}
class Error extends State {}

sealed class Event {}
class Start extends Event {}
class Stop extends Event {}
class Fail extends Event {}

State nextState(State current, Event event) {
  return switch ((current, event)) {
    (Idle(), Start()) => Active(),
    (Active(), Stop()) => Idle(),
    (Active(), Fail()) => Error(),
    (Error(), Stop()) => Idle(),
    _ => current,
  };
}

void main() {
  State current = Idle();
  print('Initial: $current');

  var events = [Start(), Fail(), Stop()];
  
  for (var e in events) {
    current = nextState(current, e);
    print('Event ${e.runtimeType} -> $current');
  }
}
```
