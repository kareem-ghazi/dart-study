# Assignments: Metadata

Practice using built-in and custom annotations in Dart.

## Assignment 1: Using @override
**Objective:** Correctly use the `@override` annotation.
*(الهدف: استخدام التعليق التوضيحي `@override` بشكل صحيح.)*

**Instructions:**
1.  Create a class `Animal` with a method `makeSound()` that prints "Some sound".
2.  Create a subclass `Dog` extending `Animal`.
3.  Override `makeSound` in `Dog` to print "Bark".
4.  Add the `@override` annotation to the `Dog`'s method.
5.  Call it in `main`.

**Expected Output:**
```
Bark
```

---

## Assignment 2: Marking as Deprecated
**Objective:** Mark a method as deprecated and provide a message.
*(الهدف: تمييز طريقة على أنها مهملة وتوفير رسالة.)*

**Instructions:**
1.  Create a class `Calculator`.
2.  Add a method `addNumbers(int a, int b)` that returns `a + b`.
3.  Mark this method with `@Deprecated('Use add() instead')`.
4.  Add a new method `add(int a, int b)`.
5.  In `main`, call `addNumbers` (your editor might cross it out or show a warning) and `add`.

**Expected Output:**
```
5
5
```

---

## Assignment 3: Custom Todo Annotation
**Objective:** Create and use a simple custom annotation.
*(الهدف: إنشاء واستخدام تعليق توضيحي مخصص بسيط.)*

**Instructions:**
1.  Define a class `Note` with a `final String message` and a `const` constructor.
2.  Annotate a function `doWork()` with `@Note('Refactor this later')`.
3.  The code itself doesn't need to use the annotation at runtime (reflection is complex), just define and apply it.
4.  Run the function `doWork` which just prints "Working...".

**Expected Output:**
```
Working...
```

---

## Assignment 4: Visible For Testing (Simulation)
**Objective:** Understand the concept of visibility for testing.
*(الهدف: فهم مفهوم الرؤية للاختبار.)*

**Instructions:**
1.  Usually `visibleForTesting` requires `package:meta`, but we can simulate the intent.
2.  Create a class `Database`.
3.  Add a method `reset()` and mark it with a comment `// @visibleForTesting`.
4.  (If you have `package:meta`, import it and use the real annotation).
5.  In `main`, print "Resetting database for test..." and call `reset()`.

**Expected Output:**
```
Resetting database for test...
Database reset.
```

---

## Assignment 5: Restricting Annotation Targets (Advanced)
**Objective:** Define an annotation that targets specific constructs.
*(الهدف: تعريف تعليق توضيحي يستهدف بناءات محددة.)*

**Instructions:**
1.  Import `package:meta/meta_meta.dart` (Note: this might not work in standard DartPad without packages, if not available, just write the code as if it were).
2.  Define an annotation class `OnFunctionOnly`.
3.  Annotate it with `@Target({TargetKind.function})`.
4.  Apply it to a top-level function.
5.  (Optional) Try applying it to a class and see if the analyzer complains (if using an IDE).

**Expected Output:**
```
(No runtime output, this is a static analysis check)
Function execution.
```

---

## Solutions

### Solution 1: Using @override

```dart
class Animal {
  void makeSound() {
    print('Some sound');
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print('Bark');
  }
}

void main() {
  Dog d = Dog();
  d.makeSound();
}
```

### Solution 2: Marking as Deprecated

```dart
class Calculator {
  @Deprecated('Use add() instead')
  int addNumbers(int a, int b) => a + b;

  int add(int a, int b) => a + b;
}

void main() {
  var calc = Calculator();
  // This line generates a warning in analysis
  print(calc.addNumbers(2, 3)); 
  print(calc.add(2, 3));
}
```

### Solution 3: Custom Todo Annotation

```dart
class Note {
  final String message;
  const Note(this.message);
}

@Note('Refactor this later')
void doWork() {
  print('Working...');
}

void main() {
  doWork();
}
```

### Solution 4: Visible For Testing

```dart
// import 'package:meta/meta.dart'; // Uncomment if package is available

class Database {
  // @visibleForTesting
  void reset() {
    print('Database reset.');
  }
}

void main() {
  print('Resetting database for test...');
  var db = Database();
  db.reset();
}
```

### Solution 5: Restricting Annotation Targets

```dart
// import 'package:meta/meta_meta.dart'; // Requires package:meta

/*
@Target({TargetKind.function})
class OnFunctionOnly {
  const OnFunctionOnly();
}

@OnFunctionOnly()
void myFunction() {
  print('Function execution.');
}
*/

void main() {
  print('Function execution.');
  // Ideally, this code is checked by the analyzer.
}
```
