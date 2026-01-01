# Constructors

## Overview
Constructors are how you build objects. Dart provides powerful tools to customize this process, including handling inheritance and initializing complex data efficiently.
(المُنشئات (Constructors) هي كيفية بناء الكائنات. توفر Dart أدوات قوية لتخصيص هذه العملية، بما في ذلك التعامل مع الوراثة وتهيئة البيانات المعقدة بكفاءة.)

---

## Initializing Formal Parameters

### Concept
You can use `this.variableName` directly in the constructor arguments to automatically assign values to instance variables. This is the most common way to write constructors.
(يمكنك استخدام `this.variableName` مباشرة في معاملات المُنشئ لتعيين القيم لمتغيرات النسخة تلقائياً. هذه هي الطريقة الأكثر شيوعاً لكتابة المُنشئات.)

### Code Example
```dart
class Point {
  double x, y;
  // Automatically assigns x and y
  Point(this.x, this.y); 
}
```
**Explanation:** `this.x` takes the first argument and puts it into the `x` variable of the object being created.
(**الشرح:** `this.x` تأخذ المعامل الأول وتضعه في المتغير `x` للكائن الذي يتم إنشاؤه.)

---

## Use an Initializer List

### Concept
An **Initializer List** allows you to set variables *before* the constructor body runs. This is crucial for initializing `final` fields or checking values with `assert`.
(**قائمة التهيئة (Initializer List)** تسمح لك بتعيين المتغيرات *قبل* تشغيل جسم المُنشئ. هذا ضروري لتهيئة الحقول النهائية `final` أو التحقق من القيم باستخدام `assert`.)

### Code Example
```dart
Point(double x, double y)
    : x = x,
      y = y,
      distance = sqrt(x*x + y*y); // Calculation before body
```
**Explanation:** The part after the colon `:` is the initializer list. It calculates `distance` and assigns `x` and `y` before the `{}` block starts.
(**الشرح:** الجزء بعد النقطتين `:` هو قائمة التهيئة. تقوم بحساب `distance` وتعيين `x` و `y` قبل أن يبدأ بلوك `{}`.)

### Analogy
Think of the initializer list as **pre-flight checks** done by a pilot before the plane engines start (constructor body). You must check fuel and flaps (final variables) before you can fly.
(تخيل قائمة التهيئة كـ **فحوصات ما قبل الطيران** التي يقوم بها الطيار قبل تشغيل المحركات (جسم المُنشئ). يجب عليك التحقق من الوقود والقلابات (المتغيرات النهائية) قبل أن تتمكن من الطيران.)

---

## Constructor Inheritance

### Concept
Constructors are **not** inherited. A subclass does not automatically get the constructors of its parent. If the parent has a constructor that requires arguments, the child must call it using `super`.
(المُنشئات **لا** تُورث. الفئة الفرعية لا تحصل تلقائياً على مُنشئات الأب. إذا كان لدى الأب مُنشئ يتطلب معاملات، يجب على الابن استدعاؤه باستخدام `super`.)

### Code Example
```dart
class Employee extends Person {
  // Must call super.fromJson because Person has no default constructor
  Employee.fromJson(Map data) : super.fromJson(data);
}
```
**Explanation:** `Employee` manually defines a constructor that forwards data to `Person`'s constructor.
(**الشرح:** `Employee` تعرف منشئاً يدوياً يقوم بتمرير البيانات إلى منشئ `Person`.)

---

## Super Parameters

### Concept
**Super Parameters** are a shortcut to pass arguments to the parent constructor. Instead of writing `: super(x, y)`, you just write `super.x`.
(**معاملات السوبر (Super Parameters)** هي اختصار لتمرير المعاملات إلى منشئ الأب. بدلاً من كتابة `: super(x, y)`، تكتب ببساطة `super.x`.)

### Code Example
```dart
class Vector3d extends Vector2d {
  double z;
  // Passes x and y to Vector2d constructor automatically
  Vector3d(super.x, super.y, this.z);
}
```
**Explanation:** `super.x` takes the value passed to `Vector3d` and immediately gives it to `Vector2d`'s constructor.
(**الشرح:** `super.x` تأخذ القيمة الممررة لـ `Vector3d` وتعطيها فوراً لمنشئ `Vector2d`.)

---

## Important Notes & Warnings

*   **Order of Execution:** Initializer list -> Super constructor -> Main constructor body. (ترتيب التنفيذ: قائمة التهيئة -> منشئ الأب -> جسم المنشئ الرئيسي.)
*   **Final Fields:** Must be initialized in the initializer list or declared with a value. (الحقول النهائية: يجب تهيئتها في قائمة التهيئة أو تعريفها بقيمة.)
*   **No `this`:** You cannot access `this` in the initializer list because the object isn't fully created yet. (لا يمكنك الوصول لـ `this` في قائمة التهيئة لأن الكائن لم يكتمل إنشاؤه بعد.)

---

## Key Takeaways

1.  **Syntactic Sugar:** `this.var` and `super.var` save you from writing repetitive code.
2.  **Initializer List:** The place for logic before the object exists (e.g., asserts, calculations).
3.  **Manual Wiring:** You must manually call super constructors if they aren't default (no-arg).
4.  **Verification:** Use `assert` in initializer lists to validate data early.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Initializer List** | Code running before constructor body. | قائمة التهيئة | `: x = 5` |
| **Super Parameter** | Shortcut to pass args to superclass. | معامل السوبر | `super.name` |
| **Super Constructor** | The constructor of the parent class. | منشئ الأب | `super()` |
| **Default Constructor** | A constructor with no arguments. | منشئ افتراضي | `Class()` |
| **Redirecting** | Calling one constructor from another. | إعادة توجيه | `Class() : this.named()` |
