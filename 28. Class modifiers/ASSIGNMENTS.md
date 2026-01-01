# Assignments: Class Modifiers

## Assignment 1: The Abstract Artist
**Objective:** Understand `abstract` classes.
(فهم الفئات المجردة.)

**Instructions:**
1.  Define an `abstract class Shape` with an abstract method `double calculateArea()`.
2.  Create a subclass `Circle` that extends `Shape`.
3.  Implement `calculateArea` for `Circle` (area = 3.14 * radius * radius).
4.  Try to instantiate `Shape` in `main` (comment out the error).
5.  Instantiate `Circle` and print its area.

**Expected Output:**
```
Circle Area: 78.5
```

## Assignment 2: The Base Foundation
**Objective:** Practice using `base` classes to enforce inheritance.
(ممارسة استخدام فئات `base` لفرض الوراثة.)

**Instructions:**
1.  Create a `base class Character` with a method `attack()`.
2.  Create a `base class Warrior` that extends `Character`.
3.  Create a class `MockCharacter` that tries to `implement Character` (this would be an error in a separate library, but for this single-file exercise, just observe the syntax or simulate the structure).
4.  *Self-Correction:* Since we are in one file, the restrictions are loose. Imagine `Character` is in `lib_a.dart`.
5.  In `main`, create a `Warrior` and call `attack()`.

**Expected Output:**
```
Warrior attacks!
```

## Assignment 3: The Interface Contract
**Objective:** Use `interface` to define a strict contract.
(استخدام `interface` لتحديد عقد صارم.)

**Instructions:**
1.  Define an `interface class Payable` with a method `calculateSalary()`.
2.  Create a class `Employee` that `implements Payable`.
3.  Override `calculateSalary` to return a fixed amount.
4.  In `main`, create an `Employee` and print the salary.

**Expected Output:**
```
Salary: 5000
```

## Assignment 4: Sealed Game States
**Objective:** Use `sealed` classes for exhaustive pattern matching.
(استخدام الفئات المختومة `sealed` لمطابقة الأنماط الشاملة.)

**Instructions:**
1.  Define a `sealed class GameState`.
2.  Define subclasses: `Playing`, `Paused`, `GameOver`.
3.  Create a function `String stateMessage(GameState state)`.
4.  Use a switch expression to return a message for each state.
5.  Test with all three states in `main`.

**Expected Output:**
```
Game is running!
Game is paused.
Game Over! Try again.
```

## Assignment 5: The Final Vault (Expert)
**Objective:** Combine modifiers and understand `final`.
(الجمع بين المعدلات وفهم `final`.)

**Instructions:**
1.  Define a `final class Vault`.
2.  Add a private property `_secretCode` and a method `access(String code)`.
3.  Try to extend `Vault` with `class BrokenVault extends Vault` (this will error if treated as outside library, or works inside. Mark `BrokenVault` as `base`, `final` or `sealed` if inside).
4.  Demonstrate that `Vault` cannot be subclassed (conceptually) by creating a secure instance in `main`.

**Expected Output:**
```
Vault accessed: true
```

---

## Solutions

```dart
// Assignment 1
abstract class Shape {
  double calculateArea();
}

class Circle extends Shape {
  final double radius;
  Circle(this.radius);

  @override
  double calculateArea() => 3.14 * radius * radius;
}

// Assignment 2
base class Character {
  void attack() => print('Character attacks!');
}

base class Warrior extends Character {
  @override
  void attack() => print('Warrior attacks!');
}

// Assignment 3
interface class Payable {
  double calculateSalary() {
    return 0;
  }
}

class Employee implements Payable {
  @override
  double calculateSalary() => 5000;
}

// Assignment 4
sealed class GameState {}
class Playing extends GameState {}
class Paused extends GameState {}
class GameOver extends GameState {}

String stateMessage(GameState state) => switch (state) {
  Playing() => 'Game is running!',
  Paused() => 'Game is paused.',
  GameOver() => 'Game Over! Try again.',
};

// Assignment 5
final class Vault {
  final String _secretCode = "1234";
  bool access(String code) => code == _secretCode;
}

void main() {
  // 1. Abstract
  // Shape s = Shape(); // Error
  var c = Circle(5);
  print('Circle Area: ${c.calculateArea()}');

  // 2. Base
  var w = Warrior();
  w.attack();

  // 3. Interface
  var e = Employee();
  print('Salary: ${e.calculateSalary()}');

  // 4. Sealed
  print(stateMessage(Playing()));
  print(stateMessage(Paused()));
  print(stateMessage(GameOver()));

  // 5. Final
  var v = Vault();
  print('Vault accessed: ${v.access("1234")}');
}
```
