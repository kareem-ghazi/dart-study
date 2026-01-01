# Extension Types

## Overview
**Extension Types** (introduced in Dart 3.3) let you wrap an existing type (like `int` or `String`) with a new name and a new set of methods, **without any performance cost**. At runtime, the wrapper disappears, and only the original data remains.
(**أنواع التوسعة (Extension Types)** (التي تم تقديمها في Dart 3.3) تسمح لك بتغليف نوع موجود (مثل `int` أو `String`) باسم جديد ومجموعة جديدة من الدوال، **بدون أي تكلفة في الأداء**. في وقت التشغيل، يختفي الغلاف، وتبقى البيانات الأصلية فقط.)

---

## Defining Extension Types

### Concept
Use `extension type Name(Type representation)`. This creates a new type checking rule at compile time.
(استخدم `extension type Name(Type representation)`. هذا ينشئ قاعدة تحقق من النوع جديدة في وقت الترجمة.)

### Code Example
```dart
extension type Id(int value) {
  bool get isValid => value > 0;
}
```
**Explanation:** `Id` looks like a class, but it's just an `int` in disguise.
(**الشرح:** `Id` يبدو كفئة، لكنه مجرد `int` متخفي.)

---

## Transparent vs Opaque

### Opaque (Default)
By default, the new type hides all methods of the original type. `Id` does NOT have `+` or `-` or `abs()`, even though it wraps an `int`. This is great for safety.
(افتراضياً، النوع الجديد يخفي جميع دوال النوع الأصلي. `Id` لا يحتوي على `+` أو `-` أو `abs()`، رغم أنه يغلف `int`. هذا ممتاز للأمان.)

### Transparent (`implements`)
If you want to keep the original methods, use `implements`.
(إذا كنت تريد الاحتفاظ بالدوال الأصلية، استخدم `implements`.)

```dart
extension type MyInt(int i) implements int {
  // Now has all int methods AND my new ones
}
```

---

## Type Erasure

### Concept
**Type Erasure** means the wrapper only exists in your code editor and compiler. When the app runs, it is literally just the underlying type.
(**محو النوع (Type Erasure)** يعني أن الغلاف موجود فقط في محرر الكود والمترجم. عندما يعمل التطبيق، هو حرفياً مجرد النوع الأساسي.)

### Code Example
```dart
var id = Id(123);
print(id.runtimeType); // int (Not Id!)
```

---

## Important Notes & Warnings

*   **Zero Cost:** Since they are erased, they use 0 extra memory. (تكلفة صفرية: بما أنه يتم محوها، فهي تستخدم 0 ذاكرة إضافية.)
*   **Runtime Safety:** `is` checks will check the underlying type. `id is int` returns true. (أمان وقت التشغيل: فحوصات `is` ستفحص النوع الأساسي. `id is int` ترجع true.)
*   **Use Cases:** Perfect for IDs, preventing unit mix-ups (Meters vs Feet), and JS interoperability. (حالات الاستخدام: مثالية للمعرفات، منع خلط الوحدات (متر مقابل قدم)، والتوافق مع JS.)

---

## Key Takeaways

1.  **Safety wrapper:** Protects `int` from being added or multiplied if it's meant to be an ID.
2.  **Performance:** Faster than a normal wrapper class.
3.  **Flexibility:** Can replace or extend the interface.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Extension Type** | A zero-cost compile-time wrapper. | نوع توسعة | `extension type E(int i)` |
| **Representation Type** | The real type hidden inside. | نوع التمثيل | `int` inside `E(int)` |
| **Type Erasure** | Removing wrapper info at runtime. | محو النوع | `E` becomes `int` |
