# Dot Shorthands

## Overview
Dart allows you to be concise. If Dart knows what type is expected, you don't need to write the type name again. You can just start with a dot `.`.
(تسمح لك Dart بالاختصار. إذا كانت Dart تعرف النوع المتوقع، فلن تحتاج لكتابة اسم النوع مرة أخرى. يمكنك فقط البدء بنقطة `.`.)

---

## Enums
### Concept
Instead of `Color.red`, just write `.red` if the variable type is already `Color`.
(بدلاً من `Color.red`، اكتب فقط `.red` إذا كان نوع المتغير هو `Color` بالفعل.)

### Code Example
```dart
enum Color { red, green, blue }
Color c = .red; // Knows it's Color (يعرف أنه Color)
```

---

## Constructors
### Concept
Use `.new()` or `.name()` to create objects without repeating the class name.
(استخدم `.new()` أو `.name()` لإنشاء كائنات دون تكرار اسم الفئة.)

### Code Example
```dart
List<int> numbers = .filled(5, 0); // List.filled
class Point { Point(int x, int y); }
Point p = .new(1, 2); // Point(1, 2)
```
**Explanation:** `List<int>` tells Dart that `.filled` belongs to `List`.
(**الشرح:** `List<int>` تخبر Dart بأن `.filled` تنتمي لـ `List`.)

---

## Static Members
### Concept
Works for static methods too, like `int.parse()`.
(تعمل مع الدوال الساكنة أيضاً، مثل `int.parse()`.)

### Code Example
```dart
int value = .parse('123');
```

---

## Rules & Limitations

### 1. Context is Key
You must have a clear type expectation. You can't just say `var x = .red;` because Dart doesn't know what `.red` belongs to.
(يجب أن يكون لديك توقع نوع واضح. لا يمكنك قول `var x = .red;` لأن Dart لا تعرف إلى ماذا تنتمي `.red`.)

### 2. Equality Checks
When checking equality, the dot shorthand must be on the **right side**.
(عند التحقق من المساواة، يجب أن يكون اختصار النقطة على **الجانب الأيمن**.)

```dart
if (myColor == .green) { ... } // OK
// if (.green == myColor) { ... } // ERROR
```

---

## Key Takeaways
1.  **Cleaner Code:** Removes noise like `Color.red`, `Color.blue`.
2.  **Less Repetition:** `MyLongClassName var = .new();` vs `MyLongClassName var = MyLongClassName();`.
3.  **Switch Statements:** Makes matching enums very clean.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Dot Shorthand** | Omitting type name when context is clear. | اختصار النقطة | `.value` |
| **Context Type** | The expected type in a specific code spot. | نوع السياق | `Color c = ...` |
