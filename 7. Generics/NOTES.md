# Generics

## Overview
**English:** Generics allow you to write flexible, reusable code that works with different types while maintaining type safety. Instead of writing separate logic for `int`, `String`, etc., you use a placeholder like `<T>`.
**Arabic:** (تسمح لك "Generics" (الأنواع العامة) بكتابة كود مرن وقابل لإعادة الاستخدام يعمل مع أنواع مختلفة مع الحفاظ على أمان النوع. بدلاً من كتابة منطق منفصل لكل من `int` و `String` وما إلى ذلك، تستخدم نائباً مثل `<T>`.)

---

## Why Use Generics?
**English:**
1.  **Type Safety:** Prevents errors like adding a string to a list of numbers.
2.  **Code Reuse:** Write logic once and use it for any type.
**Arabic:**
1.  **أمان النوع:** يمنع الأخطاء مثل إضافة نص إلى قائمة أرقام.
2.  **إعادة استخدام الكود:** اكتب المنطق مرة واحدة واستخدمه لأي نوع.

```dart
// Without Generics (unsafe) / بدون Generics (غير آمن)
var list = [];
list.add(1);
list.add('text'); // Allowed but might cause issues later

// With Generics (safe) / مع Generics (آمن)
var names = <String>[];
// names.add(1); // Compile-time Error! (خطأ وقت الترجمة!)
```

**Analogy:**
*   **English:** A generic box `<T>` is like a shipping container that is labeled. If the label says "Fruit", you can't load "Cars" into it.
*   **Arabic:** (الصندوق العام `<T>` يشبه حاوية شحن عليها ملصق. إذا كان الملصق يقول "فاكهة"، فلا يمكنك تحميل "سيارات" بداخلها.)

---

## Generic Collections
**English:** Most collections in Dart (`List`, `Set`, `Map`) are generic. You specify the type they hold inside `< >`.
**Arabic:** (معظم المجموعات في Dart (`List`, `Set`, `Map`) هي عامة. تحدد النوع الذي تحتويه داخل `< >`.)

```dart
List<String> names = ['Ali', 'Sara'];
Map<int, String> users = {1: 'Admin', 2: 'Guest'};
```

---

## Restricting Types (Bounds)
**English:** Sometimes you want to allow only specific types (e.g., only numbers). You can use `extends` to restrict the generic type.
**Arabic:** (أحياناً تريد السماح بأنواع محددة فقط (مثل الأرقام فقط). يمكنك استخدام `extends` لتقييد النوع العام.)

```dart
// T must be a subclass of Number (int or double)
// (يجب أن يكون T فئة فرعية من Number)
class Calculator<T extends num> {
  T add(T a, T b) => (a + b) as T;
}
```

---

## Generic Methods
**English:** Functions can also be generic. This allows the function to accept and return different types based on how it's called.
**Arabic:** (الدوال يمكن أن تكون عامة أيضاً. هذا يسمح للدالة بقبول وإرجاع أنواع مختلفة بناءً على كيفية استدعائها.)

```dart
T getFirst<T>(List<T> items) {
  return items[0];
}

var firstInt = getFirst<int>([1, 2, 3]); // returns int
var firstString = getFirst<String>(['a', 'b']); // returns String
```

---

## Key Takeaways
*   Generics provide stronger type checks at compile time.
*   Use single letters like `T` (Type), `E` (Element), `K` (Key), `V` (Value) for generic parameters.
*   Generics reduce code duplication.
*   Dart generics are **reified**, meaning type information exists at runtime.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Generic** | A feature to define classes/methods with a placeholder type. | عام / معمّم | `List<T>` |
| **Type Parameter** | The placeholder variable (usually `T`, `E`) representing the type. | معامل النوع | `<T>` |
| **Reified** | Type information is preserved and available at runtime. | مجسّد / حقيقي | `list is List<int>` |
| **Bound** | A restriction on what types can be used as a generic parameter. | قيد / حد | `<T extends num>` |
| **Type Safety** | Ensuring that variables only hold data of the correct type. | أمان النوع | `List<String>` |
