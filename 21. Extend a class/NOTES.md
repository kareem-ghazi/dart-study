# Extend a Class (Inheritance)

## Overview
Inheritance allows you to create a new class (child) based on an existing class (parent). The child inherits all the features of the parent and can add its own.
(الوراثة تسمح لك بإنشاء فئة جديدة (ابن) بناءً على فئة موجودة (أب). يرث الابن جميع ميزات الأب ويمكنه إضافة ميزاته الخاصة.)

---

## Basic Inheritance

### Concept
Use the `extends` keyword to define a relationship where one class "is a" type of another class.
(استخدم الكلمة المفتاحية `extends` لتعريف علاقة حيث تكون فئة ما "نوعاً من" فئة أخرى.)

### Code Example
```dart
class Animal {
  void eat() => print('Eating');
}

class Dog extends Animal {
  void bark() => print('Woof');
}
```
**Explanation:** `Dog` is an `Animal`. It can `eat()` (inherited) and `bark()` (its own).
(**الشرح:** `Dog` هو `Animal`. يمكنه أن يأكل `eat()` (موروثة) وينبح `bark()` (خاصة به).)

---

## Overriding Members

### Concept
**Overriding** allows a subclass to provide a specific implementation of a method that is already defined in its superclass. Use `@override` to prevent mistakes.
(**تجاوز (Overriding)** يسمح للفئة الفرعية بتوفير تنفيذ محدد لدالة معرفة بالفعل في فئتها العليا. استخدم `@override` لتجنب الأخطاء.)

### Code Example
```dart
class Dog extends Animal {
  @override
  void eat() {
    super.eat(); // Call original method (استدعاء الدالة الأصلية)
    print('Dog is happy');
  }
}
```
**Explanation:** `Dog` changes how `eat()` works. It calls the parent's `eat` first using `super`, then does extra stuff.
(**الشرح:** `Dog` يغير كيفية عمل `eat()`. يستدعي `eat` الخاصة بالأب أولاً باستخدام `super`، ثم يقوم بأشياء إضافية.)

### Analogy
Your father has a recipe for soup. You inherit the recipe but "override" it by adding extra spice. It's still the soup, but your version.
(والدك لديه وصفة للحساء. أنت ترث الوصفة لكن "تتجاوزها" بإضافة توابل إضافية. لا يزال الحساء، لكن بنسختك.)

---

## Covariant Keyword

### Concept
Normally, you can't tighten types in subclasses. `covariant` allows you to say "I promise I will only send a specific subtype here", overriding standard type safety rules for method parameters.
(عادة، لا يمكنك تضييق الأنواع في الفئات الفرعية. `covariant` تسمح لك بقول "أعدك بأنني سأرسل نوعاً فرعياً محدداً فقط هنا"، متجاوزاً قواعد أمان النوع القياسية لمعاملات الدوال.)

### Code Example
```dart
class Animal {
  void chase(Animal x) { ... }
}

class Mouse extends Animal { ... }

class Cat extends Animal {
  @override
  void chase(covariant Mouse x) { ... } // Only chase mice!
}
```
**Explanation:** A generic `Animal` can chase any animal, but a `Cat` specifically chases `Mouse`.
(**الشرح:** `Animal` العام يمكنه مطاردة أي حيوان، لكن `Cat` تطارد `Mouse` تحديداً.)

---

## noSuchMethod()

### Concept
This is a failsafe method called when you try to access a member that doesn't exist on an object (usually when using `dynamic`).
(هذه دالة أمان يتم استدعاؤها عندما تحاول الوصول لعضو غير موجود في كائن (عادة عند استخدام `dynamic`).)

### Code Example
```dart
@override
void noSuchMethod(Invocation invocation) {
  print('Missing: ${invocation.memberName}');
}
```
**Explanation:** Instead of crashing, the program runs this method.
(**الشرح:** بدلاً من التحطم، يشغل البرنامج هذه الدالة.)

---

## Important Notes & Warnings

*   **Single Inheritance:** Dart only supports inheriting from ONE class. Use Mixins for multiple inheritance behavior. (Dart تدعم الوراثة من فئة واحدة فقط. استخدم Mixins لسلوك الوراثة المتعددة.)
*   **Super calls:** `super.method()` calls the immediate parent's version. (يستدعي `super.method()` نسخة الأب المباشر.)
*   **Constructors:** Are NOT inherited. (المُنشئات لا تُورث.)

---

## Key Takeaways

1.  **Reusability:** Write code once in a parent class, use it in many children.
2.  **Polymorphism:** Treat a `Dog` as an `Animal`, but it behaves like a `Dog`.
3.  **Safety:** `@override` helps catch typos (e.g., if you misspell the method name, Dart warns you).
4.  **Dynamic Handling:** `noSuchMethod` allows for dynamic programming patterns.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Superclass** | The parent class being inherited from. | الفئة العليا (الأب) | `class Animal` |
| **Subclass** | The child class inheriting functionality. | الفئة الفرعية (الابن) | `class Dog extends Animal` |
| **Override** | Replacing parent behavior in child. | تجاوز | `@override void run()` |
| **Super** | Keyword to refer to the parent instance. | سوبر (الأب) | `super.run()` |
| **Covariant** | Allowing a tighter type than the parent. | متغير مشارك | `covariant MyType` |
