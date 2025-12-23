# The Dart Type System

## Overview
**English:** Dart is a "sound" typed language. This means if a variable is defined as a `String`, Dart guarantees it will only ever hold a string at runtime. It combines **Static Analysis** (checking code before running) and **Runtime Checks** (checking while running) to ensure safety.
**Arabic:** (لغة Dart هي لغة "سليمة النوع" (Sound Typed). هذا يعني أنه إذا تم تعريف متغير كـ `String`، تضمن Dart أنه سيحتوي فقط على نص وقت التشغيل. تجمع بين **التحليل الثابت** (فحص الكود قبل التشغيل) و **الفحوصات وقت التشغيل** (الفحص أثناء العمل) لضمان الأمان.)

---

## What is Soundness?
**English:** Soundness ensures your program never gets into an invalid state (like treating a number as a function). "Types can't lie."
**Arabic:** (تضمن السلامة أن برنامجك لا يدخل أبداً في حالة غير صالحة (مثل معاملة رقم كدالة). "الأنواع لا يمكن أن تكذب".)

---

## Overriding Rules
**English:** When you override a method in a subclass, there are strict rules to maintain soundness.
**Arabic:** (عندما تعيد تعريف دالة في فئة فرعية، هناك قواعد صارمة للحفاظ على السلامة.)

### 1. Return Types
**English:** You can return a **subtype** (more specific), but not a supertype.
**Arabic:** (يمكنك إرجاع **نوع فرعي** (أكثر تحديداً)، ولكن ليس نوعاً أعلى.)
*   *Parent:* returns `Animal`
*   *Child:* can return `Cat` (OK)

### 2. Parameter Types
**English:** You can accept a **supertype** (more general), but not a subtype (unless you use `covariant`).
**Arabic:** (يمكنك قبول **نوع أعلى** (أكثر عمومية)، ولكن ليس نوعاً فرعياً (إلا إذا استخدمت `covariant`).)
*   *Parent:* accepts `Animal`
*   *Child:* can accept `Object` (OK)
*   *Child:* CANNOT accept `Cat` (Error) -> Because the parent contract says it handles *any* Animal.

---

## Type Inference
**English:** You don't always have to write types. Dart can guess ("infer") them based on values.
**Arabic:** (لا يتوجب عليك دائماً كتابة الأنواع. يمكن لـ Dart تخمينها ("استنتاجها") بناءً على القيم.)

```dart
var x = 10; // Dart knows x is int
// x = "hello"; // Error!
```

---

## The `covariant` Keyword
**English:** Sometimes you *really* want a child class to accept a more specific parameter type. Use `covariant` to disable the static check (but be careful, it might crash at runtime if used wrong).
**Arabic:** (أحياناً تريد *حقاً* أن تقبل الفئة الفرعية نوع معامل أكثر تحديداً. استخدم `covariant` لتعطيل الفحص الثابت (ولكن كن حذراً، قد يتوقف البرنامج وقت التشغيل إذا استخدم بشكل خاطئ).)

```dart
class Cat extends Animal {
  // We strictly want only Mouse here, not just any Animal
  // (نريد هنا Mouse فقط، وليس أي Animal)
  @override
  void chase(covariant Mouse x) { ... } 
}
```

---

## Key Takeaways
*   **Soundness** = Reliability. If it compiles, types are likely correct.
*   **Method Overriding:** Return specific types, accept general types.
*   **Dynamic:** Use sparingly. It disables static checks.
*   **Inference:** Let Dart figure out types where obvious to save typing.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Soundness** | Guarantee that static types match runtime values. | سلامة (النوع) | `int` is always `int` |
| **Static Analysis** | Checking code errors before running it. | تحليل ثابت | Red underline in editor |
| **Runtime Check** | Checking types while the app is running. | فحص وقت التشغيل | `as String` check |
| **Inference** | Automatic deduction of data types. | استنتاج | `var i = 10;` |
| **Covariant** | Allowing a subclass to tighten a parameter type. | متغير مشارك / متغاير | `covariant Mouse x` |
| **Implicit Cast** | Automatic conversion (often from dynamic). | تحويل ضمني | `String s = dynamicVal;` |
