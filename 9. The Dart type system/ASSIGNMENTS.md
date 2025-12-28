# Assignments: The Dart Type System

## Assignment 1: Type Safety Fix (Basic)

**Objective:**
Identify and fix unsound code caused by `dynamic` and improper casting.
**(تحديد وإصلاح الكود غير السليم الناتج عن `dynamic` والتحويل غير الصحيح.)**

**Instructions:**
1.  Copy the following failing code:
    ```dart
    void printLengths(List<String> list) {
      for (var item in list) print(item.length);
    }
    void main() {
      List<dynamic> mixedList = ['Hello', 100, true];
      // printLengths(mixedList); // This line causes error
    }
    ```
2.  Fix the issue by creating a new `List<String>` that contains only the string elements from `mixedList` (you can check types manually or create a clean list).
3.  Pass the clean list to `printLengths`.
**(1. انسخ الكود الذي يحتوي على خطأ. 2. أصلح المشكلة بإنشاء قائمة `List<String>` جديدة تحتوي فقط على النصوص. 3. مرر القائمة النظيفة للدالة.)**

**Expected Output:**
```
5
```

---

## Assignment 2: Safe Method Overriding (Intermediate)

**Objective:**
Practice correct overriding rules (Return types and Parameter types).
**(ممارسة قواعد إعادة التعريف الصحيحة (أنواع الإرجاع وأنواع المعاملات).)**

**Instructions:**
1.  Create a class `Vehicle` with a method `Vehicle getBrand()` and `void refuel(Vehicle v)`.
2.  Create a subclass `Car` extending `Vehicle`.
3.  Override `getBrand` to return `Car` (Covariant return type - allowed).
4.  Override `refuel` to accept `Object v` (Contravariant parameter type - allowed).
5.  Print "Car brand" and "Refueling..." inside the methods.
6.  Instantiate `Car` and call methods to verify it compiles and runs.
**(1. أنشئ فئة `Vehicle` مع دوال محددة. 2. أنشئ فئة فرعية `Car`. 3. أعد تعريف `getBrand` لترجع `Car`. 4. أعد تعريف `refuel` لتقبل `Object`. 5. اطبع رسائل للتأكد.)**

**Expected Output:**
```
Car brand
Refueling...
```

---

## Assignment 3: Covariant Implementation (Advanced)

**Objective:**
Use the `covariant` keyword to enforce stricter parameter types in subclasses.
**(استخدام الكلمة المفتاحية `covariant` لفرض أنواع معاملات أكثر صرامة في الفئات الفرعية.)**

**Instructions:**
1.  Define a class `Animal`.
2.  Define a class `Dog` extends `Animal`.
3.  Define a class `Trainer` with a method `void train(Animal a)`.
4.  Define a class `DogTrainer` extends `Trainer`.
5.  Override `train` in `DogTrainer`. We want it to *only* accept a `Dog`, not just any `Animal`. Use the `covariant` keyword.
6.  In `main`, create a `DogTrainer`.
7.  Try to pass a `Dog` (should work).
8.  Try to pass a generic `Animal` (cast it as dynamic or ignore type warning to see runtime error, or just wrap in try-catch).
**(1. عرّف فئات `Animal` و `Dog`. 2. عرّف `Trainer` بدالة تقبل `Animal`. 3. عرّف `DogTrainer` وأعد تعريف الدالة لتقبل `Dog` فقط باستخدام ` covariant`. 4. جرب تمرير `Dog`. 5. جرب تمرير `Animal` ولاحظ النتيجة.)**

**Expected Output:**
```
Training a dog...
Error: type 'Animal' is not a subtype of type 'Dog' in type cast
```

---

## Assignment 4: Type Promotion with Flow Analysis (Advanced)

**Objective:**
Understand how Dart promotes `Object` or `dynamic` to specific types using control flow.
*(الهدف: فهم كيفية ترقية Dart لـ `Object` أو `dynamic` إلى أنواع محددة باستخدام التحكم في التدفق.)*

**Instructions:**
1. Write a function `processData(Object? data)`.
2. Use an `if` statement to check `if (data is List<int>)`.
3. Inside the `if`, Dart promotes `data` to `List<int>`. Iterate through it and calculate the sum.
4. Add an `else if` to check `if (data is String)`. Print "String length: ${data.length}".
5. Call the function with `[1, 2, 3]` and `"Hello"`.

**Expected Output:**
```
Sum: 6
String length: 5
```

---

## Assignment 5: Sound Type System Validator (Expert)

**Objective:**
Leverage sound typing, generics, and covariance to build a strictly typed data processor.
*(الهدف: الاستفادة من الكتابة السليمة، Generics، و Covariance لبناء معالج بيانات صارم النوع.)*

**Instructions:**
1.  Define an abstract class `Packet<T>`.
2.  Define `StringPacket` extending `Packet<String>` and `IntPacket` extending `Packet<int>`.
3.  Create a class `Processor` with a method `void process(covariant Packet<Object> p)`.
    *   This method accepts any Packet because of `covariant`.
4.  Inside `process`, use `if (p is StringPacket)` to print string content.
5.  Use `if (p is IntPacket)` to print the number squared.
6.  Create a list `List<Packet<Object>>` containing one of each packet.
7.  Iterate and pass them to `process`.

**Expected Output:**
```
Processing String: Hello
Processing Int: 100
```

---

## Solutions

### Solution 1: Type Safety Fix

```dart
void printLengths(List<String> list) {
  for (var item in list) print(item.length);
}

void main() {
  List<dynamic> mixedList = ['Hello', 100, true];
  
  // Create a safe List<String>
  List<String> stringList = [];
  for (var item in mixedList) {
    if (item is String) {
      stringList.add(item);
    }
  }
  
  printLengths(stringList);
}
```

### Solution 2: Safe Method Overriding

```dart
class Vehicle {
  Vehicle getBrand() => Vehicle();
  void refuel(Vehicle v) {}
}

class Car extends Vehicle {
  @override
  Car getBrand() {
    print("Car brand");
    return Car();
  }

  @override
  void refuel(Object v) {
    print("Refueling...");
  }
}

void main() {
  Car myCar = Car();
  myCar.getBrand();
  myCar.refuel("Gas"); // Object accepted
}
```

### Solution 3: Covariant Implementation

```dart
class Animal {}
class Dog extends Animal {}

class Trainer {
  void train(Animal a) {
    print("Training generic animal");
  }
}

class DogTrainer extends Trainer {
  @override
  void train(covariant Dog a) {
    print("Training a dog...");
  }
}

void main() {
  DogTrainer trainer = DogTrainer();
  trainer.train(Dog()); // Works

  try {
    // Force passing an Animal to trigger the covariant check failure
    Animal genericAnimal = Animal();
    (trainer as Trainer).train(genericAnimal); 
  } catch (e) {
    print("Error caught: $e");
  }
}
```

### Solution 4: Type Promotion with Flow Analysis

```dart
void processData(Object? data) {
  if (data is List<int>) {
    // Promoted to List<int>
    int sum = 0;
    for (var n in data) sum += n;
    print('Sum: $sum');
  } else if (data is String) {
    // Promoted to String
    print('String length: ${data.length}');
  } else {
    print('Unknown Type');
  }
}

void main() {
  processData([1, 2, 3]);
  processData("Hello");
}
```

### Solution 5: Sound Type System Validator

```dart
abstract class Packet<T> {
  final T content;
  Packet(this.content);
}

class StringPacket extends Packet<String> {
  StringPacket(super.content);
}

class IntPacket extends Packet<int> {
  IntPacket(super.content);
}

class Processor {
  // Accepts any packet holding an Object (basically any packet)
  // strict typing usually prevents Packet<String> -> Packet<Object>
  // but covariant allows runtime check flexibility here if needed.
  // Actually, Packet<String> IS A Packet<Object> in Dart if T is covariant?
  // In Dart generics are covariant by default.
  // We use `covariant` keyword to be explicit on method overrides usually,
  // but here we just accept Packet<Object> and rely on generic covariance.
  void process(Packet<Object> p) {
    if (p is StringPacket) {
      print('Processing String: ${p.content}');
    } else if (p is IntPacket) {
      print('Processing Int: ${p.content * p.content}');
    }
  }
}

void main() {
  var proc = Processor();
  
  // Dart generics are covariant: List<StringPacket> is a List<Packet<Object>>
  List<Packet<Object>> packets = [
    StringPacket('Hello'),
    IntPacket(10),
  ];
  
  for (var p in packets) {
    proc.process(p);
  }
}
```
