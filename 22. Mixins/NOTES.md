# Mixins

## Overview
Mixins are a way to reuse code in multiple classes that don't share the same inheritance chain. They allow you to "mix in" capabilities to any class.
(المزائج (Mixins) هي طريقة لإعادة استخدام الكود في فئات متعددة لا تشترك في نفس سلسلة الوراثة. تسمح لك بـ "مزج" قدرات في أي فئة.)

---

## Defining and Using Mixins

### Concept
Use `mixin` to define the reusable code and `with` to use it in a class.
(استخدم `mixin` لتعريف الكود القابل لإعادة الاستخدام و `with` لاستخدامه في فئة.)

### Code Example
```dart
mixin Swimmer {
  void swim() => print('Swimming');
}

class Duck with Swimmer {}
class Human with Swimmer {}
```
**Explanation:** Both `Duck` and `Human` can swim, even though they might inherit from different parents (Bird vs Mammal).
(**الشرح:** كل من `Duck` و `Human` يمكنهما السباحة، رغم أنهما قد يرثان من آباء مختلفين.)

### Analogy
Think of mixins as **skill chips**. You can plug a "Cooking Skill Chip" into a Robot or a Human. They don't have to be related; they just gain the ability to cook.
(تخيل المزائج كـ **شرائح مهارات**. يمكنك تركيب "شريحة مهارة الطبخ" في روبوت أو إنسان. لا يحتاجان لأن يكونا أقارب؛ هما فقط يكتسبان القدرة على الطبخ.)

---

## Constraints

### Concept
Mixins cannot have constructors. If you need a constructor, you must use a normal class (and lose some mixin flexibility).
(لا يمكن أن تحتوي المزائج على مُنشئات. إذا كنت بحاجة إلى مُنشئ، يجب عليك استخدام فئة عادية (وتفقد بعض مرونة المزائج).)

---

## The `on` Clause

### Concept
The `on` keyword restricts which classes can use your mixin. It says "This mixin only works on classes that extend X". This allows the mixin to call methods from that superclass using `super`.
(الكلمة المفتاحية `on` تقيد الفئات التي يمكنها استخدام المزج الخاص بك. تقول "هذا المزج يعمل فقط على الفئات التي ترث من X". هذا يسمح للمزج باستدعاء دوال من تلك الفئة العليا باستخدام `super`.)

### Code Example
```dart
class Musician { 
  void readNotes() { ... } 
}

mixin Pianist on Musician {
  void play() {
    super.readNotes(); // Safe because we know we are on a Musician
  }
}
```
**Explanation:** `Pianist` can only be mixed into `Musician` subclasses.
(**الشرح:** `Pianist` يمكن مزجه فقط في الفئات الفرعية لـ `Musician`.)

---

## Abstract Members in Mixins

### Concept
A mixin can demand that the class using it provides certain methods. This works like an abstract method in a class.
(يمكن للمزج أن يطلب من الفئة التي تستخدمه توفير دوال معينة. هذا يعمل مثل الدالة المجردة في الفئة.)

### Code Example
```dart
mixin Logger {
  void log(String msg); // Abstract (مجردة)
  
  void logError(String err) {
    log('ERROR: $err'); // Uses the abstract method (تستخدم الدالة المجردة)
  }
}
```

---

## Mixin Class

### Concept
In Dart 3, `mixin class` allows you to define a type that can be used **both** as a mixin (with `with`) and as a class (with `extends` or `new`).
(في Dart 3، `mixin class` تسمح لك بتعريف نوع يمكن استخدامه **كلاهما** كمزج (مع `with`) وكفئة (مع `extends` أو `new`).)

---

## Important Notes & Warnings

*   **Order Matters:** If you mix in multiple classes `with A, B`, and both have a method `foo()`, the last one (`B`) wins. (الترتيب مهم: إذا مزجت فئات متعددة `with A, B`، وكلاهما لديه دالة `foo()`، الأخير (`B`) هو الفائز.)
*   **No Constructors:** Remember, mixins are for behavior, not initialization state. (بدون منشئات: تذكر، المزائج للسلوك، ليس لحالة التهيئة.)

---

## Key Takeaways

1.  **Horizontal reuse:** Mixins share code sideways, not just down the inheritance tree.
2.  **`with`:** The keyword to apply a mixin.
3.  **`on`:** The keyword to restrict a mixin to a specific parent type.
4.  **Composition:** Favor composition (mixins) over deep inheritance hierarchies.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Mixin** | A class-like structure for reusing code. | مزج (خليط) | `mixin M { ... }` |
| **With** | Keyword to apply a mixin. | مع (يستخدم مع) | `class C with M` |
| **On** | Constraint limiting mixin usage. | على (مشروط بـ) | `mixin M on Base` |
| **Mixin Class** | A type usable as both class and mixin. | فئة مزيج | `mixin class MC` |
