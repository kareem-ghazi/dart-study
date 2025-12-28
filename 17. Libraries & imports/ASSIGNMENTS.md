# Assignments: Libraries & Imports

Practice managing dependencies and code organization in Dart.

## Assignment 1: Basic Import
**Objective:** Import a core Dart library and use its functions.
*(الهدف: استيراد مكتبة Dart أساسية واستخدام دوالها.)*

**Instructions:**
1.  Create a file (or just write the `main` function).
2.  Import the `dart:math` library.
3.  Use `Random().nextInt(100)` to generate a random number.
4.  Print "Random number: [number]".
5.  Use `sqrt(144)` (square root) and print the result.

**Expected Output (Example):**
```
Random number: 42
Square root: 12.0
```

---

## Assignment 2: Handling Name Conflicts
**Objective:** Use library prefixes to resolve conflicts.
*(الهدف: استخدام بادئات المكتبة لحل التعارضات.)*

**Instructions:**
1.  Assume we have two libraries (conceptually):
    *   `lib1` has a class `Box`.
    *   `lib2` also has a class `Box`.
2.  In a real scenario, you'd import files. Here, simulate the usage by defining two classes in `main` but pretending they come from imports with prefixes.
3.  Write code that simulates:
    ```dart
    import 'lib1.dart' as wrapping;
    import 'lib2.dart' as boxing;
    ```
4.  Create an instance of `wrapping.Box` and `boxing.Box`.
5.  Print their types or a property to show distinction.

**Expected Output:**
```
This is a Wrapping Box
This is a Boxing Box
```

---

## Assignment 3: Show and Hide
**Objective:** Control visibility using `show` and `hide`.
*(الهدف: التحكم في الرؤية باستخدام `show` و `hide`.)*

**Instructions:**
1.  Imagine a library `math_utils.dart` that contains `add()`, `subtract()`, and `secretCalculation()`.
2.  In your `main` file, write an import statement that imports `math_utils.dart` but **hides** `secretCalculation`.
3.  Write another import statement (commented out) that would **only show** `add`.
4.  Since we don't have the actual file, just write the import statements as comments or string literals to demonstrate syntax.
5.  Print "Imports defined correctly".

**Expected Output:**
```
Imports defined correctly
```

---

## Assignment 4: Deferred Loading (Simulation)
**Objective:** Write the syntax for lazy loading.
*(الهدف: كتابة صيغة التحميل الكسول.)*

**Instructions:**
1.  Write a function `loadHeavyFeature()` marked as `async`.
2.  Inside, write the syntax to load a library named `heavy` that was imported `deferred as heavy`.
3.  Since we can't actually load a deferred library in a single file script, just wrap the `await heavy.loadLibrary()` in a `try-catch` block or just write the code.
4.  Print "Loading library..." before and "Library loaded!" after.

**Expected Output:**
```
Loading library...
Library loaded!
```

---

## Assignment 5: Modular Plugin Architecture (Expert)

**Objective:**
Design a mini-plugin system using `library`, `part`, and `export` to expose a clean API while hiding implementation details.
*(الهدف: تصميم نظام إضافي مصغر باستخدام `library`، `part`، و `export` لعرض واجهة برمجة تطبيقات نظيفة مع إخفاء تفاصيل التنفيذ.)*

**Instructions:**
1.  **Conceptual Setup:** Imagine a file structure:
    *   `lib/core.dart` (The main entry point).
    *   `lib/src/engine.dart` (Internal implementation).
    *   `lib/src/utils.dart` (Internal helpers).
2.  **Implementation (Simulated):**
    *   Create a class `Engine` with a private method `_boot()`.
    *   Create a public function `startEngine()` that calls `_boot`.
    *   Use `export` to make `Engine` available but *hide* `_boot` (handled by privacy automatically) and hide internal helper classes.
3.  Write the code as if it were in `lib/core.dart` exporting elements from `src`.
4.  In `main`, show how a user would import `core.dart` and use `startEngine()`, but mention that accessing `src/engine.dart` directly is discouraged.

**Expected Output:**
```
Engine Started via Core API.
```

---

## Solutions

### Solution 1: Basic Import

```dart
import 'dart:math';

void main() {
  var random = Random();
  print('Random number: ${random.nextInt(100)}');
  print('Square root: ${sqrt(144)}');
}
```

### Solution 2: Handling Name Conflicts

```dart
// Simulating external libraries
class Box1 {
  @override
  String toString() => "Wrapping Box";
}

class Box2 {
  @override
  String toString() => "Boxing Box";
}

// In a real app:
// import 'package:lib1/box.dart' as wrapping;
// import 'package:lib2/box.dart' as boxing;

// Simulating the aliases
typedef WrappingBox = Box1;
typedef BoxingBox = Box2;

void main() {
  var b1 = WrappingBox(); // wrapping.Box()
  var b2 = BoxingBox();   // boxing.Box()
  
  print('This is a $b1');
  print('This is a $b2');
}
```

### Solution 3: Show and Hide

```dart
// import 'package:my_lib/math_utils.dart' hide secretCalculation;
// import 'package:my_lib/math_utils.dart' show add;

void main() {
  print("Imports defined correctly");
}
```

### Solution 4: Deferred Loading

```dart
// import 'package:my_lib/heavy.dart' deferred as heavy;

Future<void> loadHeavyFeature() async {
  print("Loading library...");
  // await heavy.loadLibrary(); 
  // heavy.doSomething();
  print("Library loaded!");
}

void main() async {
  await loadHeavyFeature();
}
```

### Solution 5: Modular Plugin Architecture

```dart
// --- Simulated File: lib/src/engine.dart ---
class Engine {
  void _boot() {
    print("Engine Internal Boot Sequence...");
  }
  
  void run() {
    _boot();
    print("Engine Running.");
  }
}

// --- Simulated File: lib/core.dart ---
// library core;
// export 'src/engine.dart' show Engine; 

// Public API function
void startEngine() {
  var e = Engine();
  e.run();
}

// --- Main User Code ---
void main() {
  print("Initializing via Core...");
  startEngine();
  
  // Note: Engine is accessible because we exported it.
  // _boot() is NOT accessible because it's private.
}
```
