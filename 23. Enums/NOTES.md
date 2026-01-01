# Enumerated Types (Enums)

## Overview
An **Enum** (short for Enumeration) is a special class used to represent a fixed set of constant values. Use it when a variable can only be one of a few specific options (like days of the week, colors, or status).
(**التعداد (Enum)** هو فئة خاصة تستخدم لتمثيل مجموعة ثابتة من القيم. استخدمه عندما يكون للمتغير خيارات محددة فقط (مثل أيام الأسبوع، الألوان، أو الحالة).)

---

## Simple Enums

### Concept
A basic enum just lists the possible values.
(التعداد البسيط يسرد فقط القيم الممكنة.)

### Code Example
```dart
enum Status { pending, approved, rejected }
```
**Explanation:** `Status` can only be one of these three. You can't make up a new status like `Status.unknown`.
(**الشرح:** `Status` يمكن أن يكون واحداً من هؤلاء الثلاثة فقط. لا يمكنك اختراع حالة جديدة مثل `Status.unknown`.)

### Analogy
A **Menu** at a restaurant. You can only order what's on the list (Pizza, Burger, Pasta). You can't order "Spaceship".
(**قائمة طعام** في مطعم. يمكنك طلب ما هو موجود في القائمة فقط (بيتزا، برجر، باستا). لا يمكنك طلب "سفينة فضائية".)

---

## Enhanced Enums

### Concept
Since Dart 2.17, Enums are real classes! They can have **fields**, **methods**, and **constructors**.
(منذ Dart 2.17، التعدادات هي فئات حقيقية! يمكن أن تحتوي على **حقول**، **دوال**، و **منشئات**.)

### Code Example
```dart
enum Planet {
  earth(9.8), mars(3.7);
  
  final double gravity;
  const Planet(this.gravity); // Must be const (يجب أن يكون ثابتاً)
}
```
**Explanation:** `Planet.earth` is an object that holds the value `9.8`.
(**الشرح:** `Planet.earth` هو كائن يحمل القيمة `9.8`.)

---

## Using Enums

### Properties
*   `index`: The position (0, 1, 2...). (الموقع)
*   `name`: The name as a string ("red"). (الاسم كنص)
*   `values`: A list of all options. (قائمة بكل الخيارات)

### Switch Statement
Enums work perfectly with `switch`. Dart warns you if you miss a case.
(التعدادات تعمل بشكل مثالي مع `switch`. Dart تحذرك إذا نسيت حالة.)

```dart
switch (status) {
  case Status.pending: print('Wait...');
  case Status.approved: print('Go!');
  // If rejected is missing, Dart warns you!
}
```

---

## Important Notes & Warnings

*   **Sealed:** You cannot extend or implement an Enum from outside. (مختومة: لا يمكنك وراثة أو تنفيذ التعداد من الخارج.)
*   **Const Constructors:** All enum constructors must be `const` because enum values are constants known at compile time. (جميع منشئات التعداد يجب أن تكون `const` لأن قيم التعداد هي ثوابت معروفة وقت الترجمة.)
*   **Comparisons:** Enums are compared by reference, so `Color.red == Color.red` is always true. (يتم مقارنة التعدادات بالمرجع، لذا `Color.red == Color.red` دائماً صحيح.)

---

## Key Takeaways

1.  **Type Safety:** Prevents spelling mistakes (e.g., passing "peding" instead of `Status.pending`).
2.  **Readability:** Code is easier to understand (`Color.red` vs `1`).
3.  **Power:** Enhanced enums let you bundle data (like color hex codes) with the options.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Enum** | A fixed list of constant values. | تعداد | `enum Size { S, M, L }` |
| **Enhanced Enum** | An enum with fields and methods. | تعداد محسن | `enum Size { S(1); final int x; const Size(this.x); }` |
| **Index** | The integer position of an enum value. | فهرس | `Size.S.index == 0` |
| **Values** | A list containing all enum instances. | قيم | `Size.values` |
