# Assignments: Extend a Class

## Assignment 1: Basic Inheritance (Basic)
**Objective:** Create a subclass that inherits properties.
(إنشاء فئة فرعية ترث الخصائص.)

**Instructions:**
1.  Create a class `Vehicle` with a method `move()` that prints "Moving...".
2.  Create a subclass `Bicycle` that extends `Vehicle`.
3.  Add a method `ringBell()` to `Bicycle` that prints "Ring ring!".
4.  In `main`, create a `Bicycle` and call both methods.

**Expected Output:**
```
Moving...
Ring ring!
```

---

## Assignment 2: Overriding Methods (Intermediate)
**Objective:** Customize behavior in a subclass.
(تخصيص السلوك في فئة فرعية.)

**Instructions:**
1.  Create a class `Shape` with a method `draw()` printing "Drawing Shape".
2.  Create `Circle` extending `Shape`. Override `draw()` to print "Drawing Circle".
3.  Create `Square` extending `Shape`. Override `draw()` to print "Drawing Square".
4.  In `main`, create a list of `Shape` containing one of each, and loop to call `draw()`.

**Expected Output:**
```
Drawing Circle
Drawing Square
```

---

## Assignment 3: The Super Keyword (Intermediate)
**Objective:** Extend behavior rather than replacing it.
(توسيع السلوك بدلاً من استبداله.)

**Instructions:**
1.  Create a class `Employee` with `work()` printing "Working generic tasks".
2.  Create a `Manager` extending `Employee`.
3.  Override `work()`. Call `super.work()` first, then print "Managing team".
4.  In `main`, create a Manager and call `work()`.

**Expected Output:**
```
Working generic tasks
Managing team
```

---

## Assignment 4: Covariant Parameters (Advanced)
**Objective:** Tighten parameter types in subclasses.
(تضييق أنواع المعاملات في الفئات الفرعية.)

**Instructions:**
1.  Create a class `Food`. Subclass it to `Bone`.
2.  Create a class `Animal` with `eat(Food f)`.
3.  Create a class `Dog` extending `Animal`.
4.  Override `eat` to accept `covariant Bone b`. Print "Dog eating bone".
5.  In `main`, create a Dog and feed it a Bone.

**Expected Output:**
```
Dog eating bone
```

---

## Assignment 5: Dynamic Method Handling (Expert)
**Objective:** Handle missing methods dynamically.
(التعامل مع الدوال المفقودة ديناميكياً.)

**Instructions:**
1.  Create a class `DynamicHandler`.
2.  Override `noSuchMethod`. Print "Method [name] not found!".
3.  In `main`, cast an instance of `DynamicHandler` to `dynamic`.
4.  Call a non-existent method `missingMethod()`.

**Expected Output:**
```
Method Symbol("missingMethod") not found!
```
*(Note: Output format of symbol might vary slightly depending on Dart version, e.g., just "missingMethod")*

---

## Solutions

```dart
// Assignment 1: Basic Inheritance
class Vehicle {
  void move() => print('Moving...');
}

class Bicycle extends Vehicle {
  void ringBell() => print('Ring ring!');
}

// Assignment 2: Overriding Methods
class Shape {
  void draw() => print('Drawing Shape');
}

class Circle extends Shape {
  @override
  void draw() => print('Drawing Circle');
}

class Square extends Shape {
  @override
  void draw() => print('Drawing Square');
}

// Assignment 3: The Super Keyword
class Employee {
  void work() => print('Working generic tasks');
}

class Manager extends Employee {
  @override
  void work() {
    super.work();
    print('Managing team');
  }
}

// Assignment 4: Covariant Parameters
class Food {}
class Bone extends Food {}

class Animal {
  void eat(Food f) => print('Animal eating');
}

class Dog extends Animal {
  @override
  void eat(covariant Bone b) {
    print('Dog eating bone');
  }
}

// Assignment 5: Dynamic Method Handling
class DynamicHandler {
  @override
  void noSuchMethod(Invocation invocation) {
    print('Method ${invocation.memberName} not found!');
  }
}

void main() {
  print('--- Assignment 1 ---');
  var bike = Bicycle();
  bike.move();
  bike.ringBell();

  print('\n--- Assignment 2 ---');
  List<Shape> shapes = [Circle(), Square()];
  for (var s in shapes) {
    s.draw();
  }

  print('\n--- Assignment 3 ---');
  var m = Manager();
  m.work();

  print('\n--- Assignment 4 ---');
  var d = Dog();
  d.eat(Bone());

  print('\n--- Assignment 5 ---');
  dynamic dh = DynamicHandler();
  dh.missingMethod();
}
```