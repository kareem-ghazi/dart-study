# Typedefs

## Overview
**English:** A `typedef` (type definition) or type alias allows you to create a custom name for any existing type. It makes code more readable, especially for complex types like maps of lists or specific function signatures.
**Arabic:** (يسمح لك `typedef` (تعريف النوع) أو الاسم المستعار للنوع بإنشاء اسم مخصص لأي نوع موجود. يجعل الكود أكثر قابلية للقراءة، خاصة للأنواع المعقدة مثل خرائط القوائم أو توقيعات الدوال المحددة.)

---

## What is a Typedef?
**English:** It's just a nickname for a type. It doesn't create a new class, just a new way to refer to an existing one.
**Arabic:** (إنه مجرد اسم مستعار لنوع ما. لا ينشئ فئة جديدة، بل مجرد طريقة جديدة للإشارة إلى نوع موجود.)

```dart
typedef Age = int;
Age myAge = 25; // Same as: int myAge = 25;
```

---

## Typedefs for Collections
**English:** Very useful for simplifying long generic types.
**Arabic:** (مفيد جداً لتبسيط الأنواع العامة الطويلة.)

```dart
// Instead of writing Map<String, List<int>> every time:
// (بدلاً من كتابة Map<String, List<int>> في كل مرة:)
typedef StudentGrades = Map<String, List<int>>;

StudentGrades grades = {
  'Ali': [90, 85],
  'Sara': [95, 92]
};
```

---

## Typedefs for Functions
**English:** Typedefs were originally used mostly for functions. They define a signature (parameters and return type) that functions must match.
**Arabic:** (كانت `typedefs` تستخدم في الأصل بشكل أساسي للدوال. إنها تحدد توقيعاً (المعاملات ونوع الإرجاع) يجب أن تتطابق معه الدوال.)

```dart
typedef Operation = int Function(int a, int b);

int add(int a, int b) => a + b;
int subtract(int a, int b) => a - b;

void execute(Operation op) {
  print(op(10, 5));
}

execute(add);      // 15
execute(subtract); // 5
```

---

## Key Takeaways
*   Use `typedef` to give descriptive names to complex types.
*   It supports Generics (e.g., `typedef ListOf<T> = List<T>`).
*   Ideally used for function signatures or complex nested collections.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Typedef** | A keyword to define an alias for a type. | تعريف نوع / اسم مستعار | `typedef Name = String;` |
| **Alias** | An alternative name for something. | اسم مستعار | `IntList` for `List<int>` |
| **Function Signature** | The specific pattern of a function (return type + parameters). | توقيع الدالة | `void Function(int)` |
