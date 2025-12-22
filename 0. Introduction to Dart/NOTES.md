# Introduction to Dart

## Overview
This page provides a brief introduction to the Dart language through samples of its main features, such as variables, control flow, functions, and classes.
*(تقدم هذه الصفحة مقدمة موجزة عن لغة Dart من خلال أمثلة لميزاتها الرئيسية، مثل المتغيرات، والتحكم في سير البرنامج، والدوال، والفئات.)*

---

## Hello World

- **Entry Point:** Every app requires a top-level `main()` function where the program execution starts.
  *(نقطة البداية: يحتاج كل تطبيق إلى دالة `main()` في المستوى الأعلى حيث يبدأ تنفيذ البرنامج.)*

- **Console Output:** The `print()` function displays text on the console.
  *(الإخراج: تقوم دالة `print()` بعرض النص على الشاشة.)*

```dart
void main() {
  print('Hello, World!');
}
```

💡 *Analogy:*
*Think of `main()` as the ignition key of a car. The car (program) won't start without turning the key.*
*(تشبيه: تخيل أن `main()` هي مفتاح تشغيل السيارة. السيارة (البرنامج) لن تعمل بدون إدارة المفتاح.)*

---

## Variables

- **Type Inference:** You can declare variables using `var` without specifying the type explicitly. Dart infers the type from the initial value.
  *(استنتاج النوع: يمكنك تعريف المتغيرات باستخدام `var` دون تحديد النوع صراحة. تستنتج Dart النوع من القيمة الأولية.)*

```dart
var name = 'Voyager I'; // String
var year = 1977;        // int
var antennaDiameter = 3.7; // double
var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune']; // List
var image = {
  'tags': ['saturn'],
  'url': '//path/to/saturn.jpg',
}; // Map
```

💡 *Analogy:*
*Variables are like labeled boxes. If you put a book in a box, it becomes a "book box" automatically.*
*(تشبيه: المتغيرات مثل صناديق عليها ملصقات. إذا وضعت كتابًا داخل الصندوق، يصبح "صندوق كتب" تلقائيًا.)*

---

## Control flow statements

Dart supports standard control flow statements to manage the execution logic.
*(تدعم Dart جمل التحكم القياسية لإدارة منطق التنفيذ.)*

- **If-Else:** Checks conditions.
- **Loops:** `for` and `while` loops repeat code.

```dart
if (year >= 2001) {
  print('21st century');
} else if (year >= 1901) {
  print('20th century');
}

for (final object in flybyObjects) {
  print(object);
}

for (int month = 1; month <= 12; month++) {
  print(month);
}

while (year < 2016) {
  year += 1;
}
```

---

## Functions

- **Typed Functions:** It is recommended to specify argument types and return types.
  *(الدوال محددة النوع: يُنصح بتحديد أنواع المعاملات والقيم المرجعة.)*

```dart
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

- **Arrow Syntax (`=>`):** A shorthand for functions containing a single statement.
  *(صيغة السهم: اختصار للدوال التي تحتوي على جملة واحدة فقط.)*

```dart
flybyObjects.where((name) => name.contains('turn')).forEach(print);
```
*(هنا `name` هو المعامل، والدالة ترجع نتيجة `contains` مباشرة.)*

---

## Comments

Comments are ignored by the compiler and are used to explain code.
*(يتجاهل المترجم التعليقات، وتستخدم لشرح الكود.)*

```dart
// One-line comment (تعليق سطر واحد)

/// Documentation comment used for generating docs (تعليق توثيقي)

/* 
   Block comment 
   (تعليق متعدد الأسطر)
*/
```

---

## Imports

Use `import` to access code from other libraries or files.
*(استخدم `import` للوصول إلى الكود من مكتبات أو ملفات أخرى.)*

```dart
import 'dart:math'; // Core library (مكتبة أساسية)
import 'package:test/test.dart'; // External package (حزمة خارجية)
import 'path/to/my_other_file.dart'; // Local file (ملف محلي)
```

---

## Classes

Classes are blueprints for creating objects. They contain data (properties) and methods (behavior).
*(الفئات هي مخططات لإنشاء الكائنات. تحتوي على بيانات (خصائص) ودوال (سلوك).)*

- **Constructor:** Initializes the object.
- **Getters:** Retrieve values dynamically.

```dart
class Spacecraft {
  String name;
  DateTime? launchDate;

  // Getter (خاصية للقراءة فقط)
  int? get launchYear => launchDate?.year;

  // Constructor (البناء)
  Spacecraft(this.name, this.launchDate);

  // Named Constructor (بناء مسمى)
  Spacecraft.unlaunched(String name) : this(name, null);

  void describe() {
    print('Spacecraft: $name');
    if (launchDate != null) {
      int years = DateTime.now().difference(launchDate!).inDays ~/ 365;
      print('Launched: $launchYear ($years years ago)');
    } else {
      print('Unlaunched');
    }
  }
}
```

---

## Enums

Enums define a fixed set of constant values.
*(تُعرف Enums مجموعة ثابتة من القيم.)*

```dart
enum PlanetType { terrestrial, gas, ice }
```

Enhanced enums can have fields, methods, and constructors.
*(يمكن أن تحتوي Enums المحسنة على حقول، دوال، وبنّاءات.)*

```dart
enum Planet {
  mercury(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  venus(planetType: PlanetType.terrestrial, moons: 0, hasRings: false);
  // ... other planets

  const Planet({required this.planetType, required this.moons, required this.hasRings});

  final PlanetType planetType;
  final int moons;
  final bool hasRings;
}
```

---

## Inheritance

Dart uses `extends` to create a subclass that inherits from a superclass.
*(تستخدم Dart الكلمة المفتاحية `extends` لإنشاء فئة فرعية ترث من فئة رئيسية.)*

```dart
class Orbiter extends Spacecraft {
  double altitude;

  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}
```

---

## Mixins

Mixins allow reusing code across multiple class hierarchies without inheritance.
*(تسمح Mixins بإعادة استخدام الكود عبر فئات متعددة دون استخدام الوراثة التقليدية.)*

```dart
mixin Piloted {
  int astronauts = 1;
  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}

class PilotedCraft extends Spacecraft with Piloted {
  // Now has 'astronauts' and 'describeCrew()'
}
```

---

## Interfaces and Abstract Classes

- **Implicit Interfaces:** Every class defines an interface. You can `implements` any class.
  *(واجهات ضمنية: كل فئة تُعرف واجهة. يمكنك تنفيذ أي فئة باستخدام `implements`.)*

- **Abstract Classes:** Cannot be instantiated and may contain abstract methods (without body).
  *(فئات مجردة: لا يمكن إنشاء كائنات منها وقد تحتوي على دوال مجردة.)*

```dart
abstract class Describable {
  void describe(); // Abstract method (دالة مجردة)
}
```

---

## Async

Use `async` and `await` to handle asynchronous operations (like file I/O or network requests) cleanly.
*(استخدم `async` و `await` للتعامل مع العمليات غير المتزامنة بشكل نظيف.)*

```dart
Future<void> printWithDelay(String message) async {
  await Future.delayed(Duration(seconds: 1)); // Wait 1 second (انتظر ثانية واحدة)
  print(message);
}
```

💡 *Analogy:*
*`await` is like pausing a video to answer the door. You stop execution, handle the external task (door), and then resume.*
*(تشبيه: `await` مثل إيقاف الفيديو لفتح الباب. توقف التنفيذ، تنهي المهمة الخارجية، ثم تكمل.)*

---

## Exceptions

Use `throw` to raise errors and `try-catch` to handle them.
*(استخدم `throw` لإطلاق الأخطاء و `try-catch` لمعالجتها.)*

```dart
try {
  if (astronauts == 0) throw StateError('No astronauts.');
} catch (e) {
  print('Error: $e');
}
```

---

## Important concepts

1. **Everything is an Object:** Variables store objects (instances of classes). Even numbers and functions are objects.
   *(كل شيء عبارة عن كائن: المتغيرات تخزن كائنات. حتى الأرقام والدوال هي كائنات.)*

2. **Null Safety:** Variables cannot be null unless you explicitly allow it using `?`.
   *(أمان Null: لا يمكن للمتغيرات أن تكون فارغة null إلا إذا سمحت بذلك باستخدام `?`.)*
   * `String? name` (Can be null / ممكن أن يكون null)
   * `String name` (Cannot be null / لا يمكن أن يكون null)

3. **Top-level functions:** Functions like `main()` can exist outside classes.
   *(دوال المستوى الأعلى: يمكن أن توجد دوال مثل `main` خارج الفئات.)*

4. **Privacy:** Identifiers starting with `_` are private to the library.
   *(الخصوصية: الأسماء التي تبدأ بـ `_` تكون خاصة بالمكتبة.)*

---

## Key Takeaways

- Dart execution starts at the `main()` function.
  *(يبدأ تنفيذ Dart من الدالة main.)*
- Dart is strongly typed but supports type inference (`var`).
  *(لغة Dart قوية النوع لكنها تدعم الاستنتاج باستخدام var.)*
- Everything in Dart is an Object.
  *(كل شيء في Dart عبارة عن كائن.)*
- Null Safety helps prevent null reference errors.
  *(يساعد نظام أمان Null في منع أخطاء القيم الفارغة.)*
- `async`/`await` simplify asynchronous code handling.
  *(تبسط async/await التعامل مع الكود غير المتزامن.)*

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Variable** | A container for storing data. | متغير | `var x = 10;` |
| **Function** | A block of code that performs a task. | دالة | `void main() {...}` |
| **Class** | A blueprint for creating objects. | فئة / كلاس | `class Car {...}` |
| **Mixin** | A way to reuse code in multiple classes. | Mixin (خليط) | `with Piloted` |
| **Async** | Keyword for asynchronous functions. | غير متزامن | `futureFunc() async` |
| **Exception** | An error that occurs during execution. | استثناء | `throw Error();` |
| **Null Safety** | Prevents variables from being null unintentionally. | أمان القيم الفارغة | `int? x;` |
