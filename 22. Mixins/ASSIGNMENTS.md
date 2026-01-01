# Assignments: Mixins

## Assignment 1: Basic Mixin (Basic)
**Objective:** Add capabilities to unrelated classes.
(إضافة قدرات لفئات غير مرتبطة.)

**Instructions:**
1.  Create a mixin `Swimmer` with `swim()` printing "Swimming...".
2.  Create a mixin `Flyer` with `fly()` printing "Flying...".
3.  Create a class `Duck` that uses both.
4.  Create a class `Fish` that uses only `Swimmer`.
5.  In `main`, test methods for both.

**Expected Output:**
```
Duck:
Swimming...
Flying...
Fish:
Swimming...
```

---

## Assignment 2: Abstract Members in Mixin (Intermediate)
**Objective:** Force the host class to implement a method.
(إجبار الفئة المستضيفة على تنفيذ دالة.)

**Instructions:**
1.  Create a mixin `Logger`.
2.  Add an abstract method `logMessage(String msg)`.
3.  Add a method `logError(String err)` that calls `logMessage('ERROR: $err')`.
4.  Create a class `ConsoleLogger` using `Logger` and implement `logMessage` to print to console.
5.  In `main`, call `logError`.

**Expected Output:**
```
ERROR: Something broke!
```

---

## Assignment 3: The 'on' Clause (Intermediate)
**Objective:** Restrict a mixin to specific subclasses.
(تقييد المزج بفئات فرعية محددة.)

**Instructions:**
1.  Create a class `Person` with `name`.
2.  Create a mixin `Coder` **on** `Person`.
3.  In `Coder`, add `code()` method that prints "$name is coding.".
4.  Create a class `Developer` extending `Person` with `Coder`.
5.  In `main`, create a Developer and call `code()`.

**Expected Output:**
```
Ali is coding.
```

---

## Assignment 4: Mixin Class (Advanced)
**Objective:** Use a type as both a class and a mixin.
(استخدام نوع كفئة وكمزج معاً.)

**Instructions:**
1.  Create a `mixin class Timestamp`.
2.  Add a method `now()` returning `DateTime.now()`.
3.  Create a class `Post` that **extends** `Timestamp`.
4.  Create a class `Comment` that uses `Timestamp` with **with**.
5.  In `main`, call `now()` on both.

**Expected Output:**
```
Post time: ...
Comment time: ...
```

---

## Assignment 5: Multiple Mixin Order (Expert)
**Objective:** Understand execution order when mixing multiple sources.
(فهم ترتيب التنفيذ عند مزج مصادر متعددة.)

**Instructions:**
1.  Create a class `Base` with `init()` printing "Base".
2.  Create mixin `A` on `Base`. Override `init()`: print "A", then `super.init()`.
3.  Create mixin `B` on `Base`. Override `init()`: print "B", then `super.init()`.
4.  Create `class C extends Base with A, B`.
5.  Create `class D extends Base with B, A`.
6.  In `main`, call `init()` on C and D. Observe the order.

**Expected Output:**
```
Class C:
B
A
Base

Class D:
A
B
Base
```

---

## Solutions

```dart
// Assignment 1: Basic Mixin
mixin Swimmer {
  void swim() => print('Swimming...');
}

mixin Flyer {
  void fly() => print('Flying...');
}

class Duck with Swimmer, Flyer {}

class Fish with Swimmer {}

// Assignment 2: Abstract Members
mixin Logger {
  void logMessage(String msg);

  void logError(String err) {
    logMessage('ERROR: $err');
  }
}

class ConsoleLogger with Logger {
  @override
  void logMessage(String msg) {
    print(msg);
  }
}

// Assignment 3: The 'on' Clause
class Person {
  String name;
  Person(this.name);
}

mixin Coder on Person {
  void code() {
    print('$name is coding.');
  }
}

class Developer extends Person with Coder {
  Developer(String name) : super(name);
}

// Assignment 4: Mixin Class
mixin class Timestamp {
  DateTime now() => DateTime.now();
}

class Post extends Timestamp {} // As class

class Comment with Timestamp {} // As mixin

// Assignment 5: Multiple Mixin Order
class Base {
  void init() => print('Base');
}

mixin A on Base {
  @override
  void init() {
    print('A');
    super.init();
  }
}

mixin B on Base {
  @override
  void init() {
    print('B');
    super.init();
  }
}

class C extends Base with A, B {}

class D extends Base with B, A {}

void main() {
  print('--- Assignment 1 ---');
  var duck = Duck();
  print('Duck:');
  duck.swim();
  duck.fly();
  var fish = Fish();
  print('Fish:');
  fish.swim();

  print('\n--- Assignment 2 ---');
  var logger = ConsoleLogger();
  logger.logError('Something broke!');

  print('\n--- Assignment 3 ---');
  var dev = Developer('Ali');
  dev.code();

  print('\n--- Assignment 4 ---');
  print('Post time: ${Post().now()}');
  print('Comment time: ${Comment().now()}');

  print('\n--- Assignment 5 ---');
  print('Class C (with A, B):');
  C().init(); // B calls A, A calls Base
  print('\nClass D (with B, A):');
  D().init(); // A calls B, B calls Base
}
```