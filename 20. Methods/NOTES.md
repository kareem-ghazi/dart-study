# Methods

## Overview
Methods are simply functions that live inside a class. They define what an object can **do**, while variables define what an object **knows**.
(الدوال (Methods) هي ببساطة وظائف تعيش داخل الفئة. هي تحدد ما يمكن للكائن **فعله**، بينما تحدد المتغيرات ما **يعرفه** الكائن.)

---

## Instance Methods

### Concept
**Instance Methods** operate on a specific object. They can access the object's data (fields) and use `this`.
(**دوال النسخة (Instance Methods)** تعمل على كائن محدد. يمكنها الوصول لبيانات الكائن (الحقول) واستخدام `this`.)

### Code Example
```dart
class Point {
  double x, y;
  Point(this.x, this.y);
  
  double distanceTo(Point other) { ... }
}
```
**Explanation:** `distanceTo` is an instance method because it calculates distance relative to a specific point (`this`).
(**الشرح:** `distanceTo` هي دالة نسخة لأنها تحسب المسافة بالنسبة لنقطة محددة (`this`).)

---

## Operators

### Concept
Dart allows you to **overload operators**. This means you can define what `+`, `-`, or `==` does for your own classes.
(تسمح لك Dart بـ **تحميل المعاملات بشكل زائد (Operator Overloading)**. هذا يعني أنه يمكنك تحديد ما يفعله `+`، `-`، أو `==` لفئاتك الخاصة.)

### Code Example
```dart
Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
```
**Explanation:** This defines that when you write `vector1 + vector2`, it returns a new vector combining their x and y values.
(**الشرح:** هذا يحدد أنه عندما تكتب `vector1 + vector2`، فإنها تعيد متجهاً جديداً يجمع قيم x و y الخاصة بهما.)

### Analogy
Teaching a dog new tricks. Usually, "Shake" means shake hands. But for a specific dog (class), you can teach "Shake" (operator) to mean "Shake body". You redefine the standard action.
(تعليم كلب حيل جديدة. عادة، "صافح" تعني مد اليد. لكن لكلب معين (فئة)، يمكنك تعليم "صافح" (المعامل) لتعني "هز جسمك". أنت تعيد تعريف الفعل القياسي.)

---

## Getters and Setters

### Concept
**Getters and Setters** allow you to control access to variables. You can calculate a value when it's accessed (getter) or run logic when it's changed (setter).
(**الجوالب والضوابط (Getters and Setters)** تسمح لك بالتحكم في الوصول للمتغيرات. يمكنك حساب قيمة عند طلبها (getter) أو تشغيل منطق عند تغييرها (setter).)

### Code Example
```dart
double get area => width * height;
set width(double value) {
  if (value > 0) _width = value;
}
```
**Explanation:** `area` looks like a variable but is calculated. `width` setter validates the input before assigning it.
(**الشرح:** `area` تبدو كمتغير لكنها محسوبة. ضابط `width` يتحقق من المدخلات قبل تعيينها.)

---

## Abstract Methods

### Concept
**Abstract Methods** have no body. They exist only in abstract classes and force subclasses to provide the implementation.
(**الدوال المجردة (Abstract Methods)** ليس لها جسم. توجد فقط في الفئات المجردة وتجبر الفئات الفرعية على توفير التنفيذ.)

### Code Example
```dart
abstract class Animal {
  void makeSound(); // No body (بدون جسم)
}
```
**Explanation:** Every `Animal` *must* make a sound, but the specific sound depends on the subclass (Dog, Cat, etc.).
(**الشرح:** كل `Animal` *يجب* أن يصدر صوتاً، لكن الصوت المحدد يعتمد على الفئة الفرعية.)

---

## Important Notes & Warnings

*   **Operator `==`:** If you override `==`, you should also override `hashCode`. (إذا قمت بتجاوز `==`، يجب عليك أيضاً تجاوز `hashCode`.)
*   **Getters vs Functions:** Use a getter (`get`) if the operation is cheap and feels like reading a property. Use a function if it does heavy work. (استخدم الجالب إذا كانت العملية خفيفة وتشبه قراءة خاصية. استخدم دالة إذا كانت تقوم بعمل ثقيل.)
*   **Encapsulation:** Start with public fields. Change to getters/setters later if needed without breaking code. (ابدأ بحقول عامة. حولها لجوالب/ضوابط لاحقاً إذا لزم الأمر دون كسر الكود.)

---

## Key Takeaways

1.  **Behavior:** Methods give objects life.
2.  **Custom Math:** Use operator overloading to make your classes work with standard math symbols.
3.  **Computed Properties:** Use getters to derive values dynamically.
4.  **Validation:** Use setters to protect your data from bad values.
5.  **Contracts:** Abstract methods define "what" must be done, not "how".

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Instance Method** | A function acting on an object instance. | دالة نسخة | `obj.method()` |
| **Operator Overloading** | Customizing standard operators (+, -). | تحميل المعاملات | `operator +` |
| **Getter** | A method that reads a property. | جالب | `get x => ...` |
| **Setter** | A method that writes a property. | ضابط | `set x(val) { ... }` |
| **Abstract Method** | A method declaration without code. | دالة مجردة | `void run();` |
