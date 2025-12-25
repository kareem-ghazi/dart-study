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

## Assignment 4: Ternary Logic (Conditional operator)

**Objective:**
Use the `? :` operator for concise conditional logic.
*(الهدف: استخدام المعامل `? :` لمنطق شرطي موجز.)*

**Instructions:**
1. Define `int age = 17`.
2. Create a string `status` that is "Adult" if `age >= 18` and "Minor" otherwise.
3. Print `status`.

**Expected Output:**
```
Minor
```

---

## Assignment 5: If-Case List (Pattern matching in if)

**Objective:**
Use `if case` to match a list pattern.
*(الهدف: استخدام `if case` لمطابقة نمط قائمة.)*

**Instructions:**
1. Create a `List<int> numbers = [1, 2]`.
2. Use `if (numbers case [int a, int b])` to check if it has exactly two integers.
3. If so, print their sum.

**Expected Output:**
```
Sum: 3
```

---

## Solutions

```dart
// Assignment 1
String calculateGrade(int score) {
  if (score >= 90) return 'A';
  if (score >= 80) return 'B';
  if (score >= 70) return 'C';
  if (score >= 60) return 'D';
  return 'F';
}

void assignment1() {
  print('--- Grade Calculator ---');
  var scores = [95, 82, 40];
  for (var s in scores) {
    print('$s is ${calculateGrade(s)}');
  }
}

// Assignment 2
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

void assignment2() {
  print('\n--- Command Handler ---');
  handleCommand('START');
  handleCommand('RESET');
}

// Assignment 3
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

void assignment3() {
  print('\n--- Payment Processor ---');
  print('Cash: \$${processPayment(100, Cash())}');
  print('Credit Card: \$${processPayment(100, CreditCard(2.5))}');
}

// Assignment 4
void assignment4() {
  int age = 17;
  String status = (age >= 18) ? "Adult" : "Minor";
  print(status);
}

// Assignment 5
void assignment5() {
  List<int> numbers = [1, 2];
  if (numbers case [int a, int b]) {
    print('Sum: ${a + b}');
  }
}

void main() {
  assignment1();
  assignment2();
  assignment3();
  print('\n--- Assignment 4 ---');
  assignment4();
  print('\n--- Assignment 5 ---');
  assignment5();
}
```