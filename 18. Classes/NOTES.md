# Classes

## Overview
Dart is an object-oriented language, meaning everything is an object built from a "blueprint" called a class. Classes bundle data (fields) and behavior (methods) together.
(Dart هي لغة كائنية التوجيه (Object-Oriented)، مما يعني أن كل شيء هو عبارة عن "كائن" (Object) مبني من "مخطط" يسمى "الفئة" (Class). تجمع الفئات البيانات (الحقول) والسلوك (الطرق) معًا.)

---

## Using class members

### Concept
**Members** are the variables and methods inside a class. You access them using a dot (`.`).
(**الأعضاء (Members)** هي المتغيرات والدوال الموجودة داخل الفئة. يمكنك الوصول إليها باستخدام النقطة (`.`).)

### Code Example
```dart
var p = Point(2, 2);
assert(p.y == 2); // Accessing instance variable (الوصول لمتغير)
double distance = p.distanceTo(Point(4, 4)); // Invoking a method (استدعاء دالة)
```
**Explanation:** `p` is an object. `p.y` gets the value of `y`. `p.distanceTo(...)` calls the method.
(**الشرح:** `p` هو كائن. `p.y` يجلب قيمة `y`. `p.distanceTo(...)` تستدعي الدالة.)

### Analogy
Think of a class as a **Smart Home Controller**. The buttons (methods) and the screen showing temperature (variables) are its **members**. You press a button (`.method()`) to do something.
(تخيل الفئة كـ **جهاز تحكم ذكي للمنزل**. الأزرار (الدوال) والشاشة التي تعرض درجة الحرارة (المتغيرات) هي **الأعضاء**. تضغط على زر (`.method()`) للقيام بشيء ما.)

---

## Using constructors

### Concept
A **Constructor** is a special method that runs when you create a new object. It builds or "constructs" the instance.
(**المُنشئ (Constructor)** هو دالة خاصة تعمل عند إنشاء كائن جديد. تقوم ببناء أو "تجهيز" النسخة.)

### Code Example
```dart
var p1 = Point(2, 2); // Standard constructor (منشئ عادي)
var p2 = Point.fromJson({'x': 1, 'y': 2}); // Named constructor (منشئ مسمى)
```
**Explanation:** `Point(2, 2)` creates a new Point. `Point.fromJson(...)` is a specific way to create a Point from data.
(**الشرح:** `Point(2, 2)` ينشئ نقطة جديدة. `Point.fromJson(...)` هي طريقة محددة لإنشاء نقطة من بيانات.)

---

## Instance variables

### Concept
**Instance Variables** (or fields) store data specific to an object. Each object has its own copy of these variables.
(**متغيرات النسخة (Instance Variables)** تخزن بيانات خاصة بالكائن. كل كائن لديه نسخته الخاصة من هذه المتغيرات.)

### Code Example
```dart
class Point {
  double? x; // Nullable, starts as null (يقبل القيمة الفارغة)
  double z = 0; // Initialized to 0 (مهيأ بقيمة 0)
}
```
**Explanation:** `x` can be null. `z` starts at 0 for every new Point unless changed.
(**الشرح:** `x` يمكن أن تكون فارغة (null). `z` تبدأ بـ 0 لكل نقطة جديدة ما لم يتم تغييرها.)

### Final Fields
If a variable is `final`, it can only be set once.
(إذا كان المتغير `final`، يمكن تعيين قيمته مرة واحدة فقط.)

---

## Implicit interfaces

### Concept
Every class in Dart acts as an **Interface**. You can implement any class to enforce its structure without inheriting its logic.
(كل فئة في Dart تعمل كـ **واجهة (Interface)**. يمكنك تنفيذ (implement) أي فئة لإجبار الكائن على اتباع هيكلها دون وراثة منطقها.)

### Code Example
```dart
class Impostor implements Person {
  String get _name => '';
  String greet(String who) => 'Hi $who. Do you know who I am?';
}
```
**Explanation:** `Impostor` must have all methods/variables that `Person` has, but defines its own behavior.
(**الشرح:** `Impostor` يجب أن يحتوي على كل دوال/متغيرات `Person`، لكنه يعرف سلوكه الخاص.)

---

## Class variables and methods (Static)

### Concept
**Static** members belong to the class itself, not to any specific object. They are shared across all instances.
(**الأعضاء الساكنة (Static)** تنتمي للفئة نفسها، وليس لكائن محدد. هي مشتركة بين جميع النسخ.)

### Code Example
```dart
class Queue {
  static const initialCapacity = 16;
}
print(Queue.initialCapacity);
```
**Explanation:** You access `initialCapacity` using the class name `Queue`, not an object variable.
(**الشرح:** تصل لـ `initialCapacity` باستخدام اسم الفئة `Queue`، وليس متغير كائن.)

---

## Important Notes & Warnings

*   **Instance vs Static:** Use `static` for constants or utilities unrelated to specific object data. (استخدم `static` للثوابت أو الأدوات غير المرتبطة ببيانات كائن محدد.)
*   **Null Safety:** Variables declared without `?` must be initialized immediately or in the constructor. (المتغيرات المعرفة بدون `?` يجب تهيئتها فوراً أو في المنشئ.)
*   **Constructors:** If you don't define a constructor, Dart provides a default empty one. (إذا لم تعرف منشئاً، توفر Dart واحداً افتراضياً فارغاً.)

---

## Key Takeaways

1.  **Everything is an Object:** All classes inherit from `Object`.
2.  **Dot Notation:** Use `.` to access members and `?.` to access safely if null.
3.  **Constructors:** Build objects; can be named (e.g., `Class.fromMap()`).
4.  **Interfaces are Implicit:** Any class can be used as an interface with `implements`.
5.  **Static Members:** Belong to the blueprint (class), not the house (object).
6.  **Final Variables:** Set once, never changed.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Class** | A blueprint for creating objects. | فئة (مخطط) | `class Car { ... }` |
| **Object** | An instance created from a class. | كائن | `var c = Car();` |
| **Instance Variable** | Data stored inside an object. | متغير نسخة | `String color;` |
| **Method** | A function defined inside a class. | دالة (طريقة) | `void drive() { ... }` |
| **Constructor** | A method to initialize an object. | مُنشئ | `Car(this.color);` |
| **Static** | Belongs to the class, shared by all objects. | ساكن (مشترك) | `static int count;` |
| **Interface** | A contract enforcing structure. | واجهة | `implements Person` |
