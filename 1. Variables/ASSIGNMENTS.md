# Assignments: Variables

## Assignment 1: Profile Creator (Basic)

**Objective:**
Practice declaring variables with explicit types and type inference (`var`).
*(الهدف: التدرب على تعريف المتغيرات بأنواع صريحة وباستخدام الاستنتاج `var`.)*

**Instructions:**
1. Declare a `String` variable named `firstName` and assign your name.
2. Declare an `int` variable named `age` and assign your age.
3. Declare a `double` variable named `height` and assign a value (e.g., 1.75).
4. Declare a variable using `var` named `isStudent` and assign a boolean value (`true` or `false`).
5. Print a single sentence using all these variables (e.g., "My name is [name], I am [age] years old...").

**Expected Output:**
```
My name is Kareem, I am 25 years old, 1.75m tall, and it is true that I am a student.
```

---

## Assignment 2: The Latecomer (Intermediate)

**Objective:**
Understand the `late` keyword and deferred initialization.
*(الهدف: فهم الكلمة المفتاحية `late` والتهيئة المؤجلة.)*

**Instructions:**
1. Declare a variable `late String biography`.
2. Create a function `void loadBiography()` that assigns a value to `biography` (e.g., "Born in 1990...").
3. In `main`, try to print `biography` *before* calling `loadBiography()`.
   *   *Note: This will cause an error. Wrap it in a try-catch block to handle the LateInitializationError.*
4. Call `loadBiography()`.
5. Print `biography` again.

**Expected Output:**
```
Error: LateInitializationError: Field 'biography' has not been initialized.
Biography: Born in 1990...
```

---

## Assignment 3: Constant Constants (Advanced)

**Objective:**
Differentiate between `final` and `const` and understand immutability.
*(الهدف: التفريق بين `final` و `const` وفهم عدم قابلية التغيير.)*

**Instructions:**
1. Declare a `const` variable `pi` with value `3.14159`.
2. Declare a `final` variable `radius` and assign it `DateTime.now().second` (simulating a changing value).
3. Calculate the area (`pi * radius * radius`) and print it.
4. Create a `const` List named `fixedList` with values `[1, 2, 3]`.
5. Try to add a number to `fixedList` inside a `try-catch` block to observe the error.

**Expected Output:**
```
Radius: 15 (example)
Area: 706.85...
Error: Unsupported operation: Cannot add to an unmodifiable list
```

---

## Assignment 4: Type Promotion (Advanced)

**Objective:**
Understand how Dart promotes types in control flows.
*(الهدف: فهم كيفية ترقية الأنواع في تدفق التحكم في Dart.)*

**Instructions:**
1. Declare a variable `Object value = "Hello Dart"`.
2. Try to access `.length` directly on `value` (comment out the line if it causes an error, noting why).
3. Use an `if` check (`is String`) to check if `value` is a String.
4. Inside the `if` block, print `value.length` (Dart knows it's a String now).
5. Assign `100` to `value` (since it's an Object).
6. Use another `if` check (`is int`) and print "It is an integer: $value".

**Expected Output:**
```
Length of string: 10
It is an integer: 100
```

---

## Assignment 5: Variable Lifecycle Simulator (Expert)

**Objective:**
Simulate a memory management system using `late`, `final`, `const`, and nullable variables to understand lifecycle and state.
*(الهدف: محاكاة نظام إدارة ذاكرة باستخدام `late`، `final`، `const`، والمتغيرات القابلة للفراغ لفهم دورة الحياة والحالة.)*

**Instructions:**
1.  Create a class `MemoryBlock` with a `final int id`.
2.  Create a class `System`.
3.  Inside `System`, define:
    *   A `const` configuration Map `{ 'max_memory': 1024 }`.
    *   A `late String bootLog`.
    *   A nullable `MemoryBlock? activeBlock`.
4.  Add a method `boot()`:
    *   Assign a value to `bootLog`.
    *   Print `bootLog`.
5.  Add a method `allocate(int id)`:
    *   If `activeBlock` is not null, throw exception "Memory leak!".
    *   Assign a new `MemoryBlock(id)` to `activeBlock`.
6.  Add a method `free()`:
    *   Set `activeBlock` to `null`.
7.  In `main`:
    *   Create a `System`.
    *   Try accessing `bootLog` before `boot()` (catch error).
    *   Boot the system.
    *   Allocate block 1, try allocating block 2 (catch error), free, allocate block 2.

**Expected Output:**
```
Error: LateInitializationError...
System booting...
Allocated Block 1
Error: Memory leak!
Freed memory.
Allocated Block 2
```

---

## Solutions

### Solution 1: Profile Creator

```dart
void main() {
  String firstName = 'Kareem';
  int age = 25;
  double height = 1.75;
  var isStudent = true;

  print('My name is $firstName, I am $age years old, $height m tall, and it is $isStudent that I am a student.');
}
```

### Solution 2: The Latecomer

```dart
late String biography;

void loadBiography() {
  biography = 'Born in 1990, loved coding ever since.';
}

void main() {
  // Attempt 1: Before initialization
  try {
    print(biography);
  } catch (e) {
    print('Error: $e');
  }

  // Initialize
  loadBiography();

  // Attempt 2: After initialization
  print('Biography: $biography');
}
```

### Solution 3: Constant Constants

```dart
void main() {
  const pi = 3.14159;
  
  // radius is final because it's determined at runtime
  final radius = DateTime.now().second; 
  
  print('Radius: $radius');
  print('Area: ${pi * radius * radius}');

  // Const list is immutable
  const fixedList = [1, 2, 3];

  try {
    fixedList.add(4);
  } catch (e) {
    print('Error: $e');
  }
}
```

### Solution 4: Type Promotion

```dart
void main() {
  Object value = "Hello Dart";
  
  // print(value.length); // Error: The getter 'length' isn't defined for the class 'Object'.
  
  if (value is String) {
    // Type promoted to String automatically
    print('Length of string: ${value.length}');
  }
  
  value = 100;
  if (value is int) {
    print('It is an integer: $value');
  }
}
```

### Solution 5: Variable Lifecycle Simulator

```dart
class MemoryBlock {
  final int id;
  MemoryBlock(this.id);
}

class System {
  static const config = {'max_memory': 1024};
  late String bootLog;
  MemoryBlock? activeBlock;

  void boot() {
    bootLog = "System booting at ${DateTime.now()}";
    print(bootLog);
  }

  void allocate(int id) {
    if (activeBlock != null) {
      throw Exception("Memory leak! Block ${activeBlock!.id} not freed.");
    }
    activeBlock = MemoryBlock(id);
    print("Allocated Block $id");
  }

  void free() {
    activeBlock = null;
    print("Freed memory.");
  }
}

void main() {
  var sys = System();

  // 1. Late Error
  try {
    print(sys.bootLog);
  } catch (e) {
    print("Error: $e");
  }

  // 2. Boot
  sys.boot();

  // 3. Allocation logic
  try {
    sys.allocate(1);
    sys.allocate(2); // Should fail
  } catch (e) {
    print("Error: $e");
  }

  // 4. Proper cycle
  sys.free();
  sys.allocate(2);
}
```
