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
**(1. عرّف فئات `Animal` و `Dog`. 2. عرّف `Trainer` بدالة تقبل `Animal`. 3. عرّف `DogTrainer` وأعد تعريف الدالة لتقبل `Dog` فقط باستخدام `covariant`. 4. جرب تمرير `Dog`. 5. جرب تمرير `Animal` ولاحظ النتيجة.)**

**Expected Output:**
```
Training a dog...
Error: type 'Animal' is not a subtype of type 'Dog' in type cast
```

---

## Solutions

```dart
// --- Assignment 2 Classes ---
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

// --- Assignment 3 Classes ---
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

// --- Assignment 1 Helper ---
void printLengths(List<String> list) {
  for (var item in list) print(item.length);
}

void main() {
  // --- Assignment 1 Solution ---
  print('--- Assignment 1 ---');
  List<dynamic> mixedList = ['Hello', 100, true];
  
  // Create a safe List<String>
  List<String> stringList = [];
  for (var item in mixedList) {
    if (item is String) {
      stringList.add(item);
    }
  }
  
  printLengths(stringList);
  print('\n');

  // --- Assignment 2 Solution ---
  print('--- Assignment 2 ---');
  Car myCar = Car();
  myCar.getBrand();
  myCar.refuel("Gas"); // Object accepted
  print('\n');

  // --- Assignment 3 Solution ---
  print('--- Assignment 3 ---');
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