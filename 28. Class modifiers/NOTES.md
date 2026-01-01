# Class modifiers

## Overview

Class modifiers in Dart control how a class can be used, extended, or implemented, both within its own library and from outside libraries. They are essential for defining robust APIs and enforcing architectural rules.

(تتحكم معدلات الفئات في Dart في كيفية استخدام الفئة أو توسيعها أو تنفيذها، سواء داخل مكتبتها الخاصة أو من مكتبات خارجية. وهي ضرورية لتحديد واجهات برمجة تطبيقات قوية وفرض قواعد هيكلية.)

## No modifier

If you define a class without any modifier, it is fully open.

(إذا قمت بتعريف فئة بدون أي معدل، فهي مفتوحة تمامًا.)

*   **English:** Can be constructed, extended, and implemented from anywhere.
*   **Arabic:** (يمكن إنشاؤها، وتوسيعها، وتنفيذها من أي مكان.)

## `abstract`

**Concept:** Abstract classes are incomplete blueprints.
(الفئات المجردة هي مخططات غير مكتملة.)

```dart
abstract class Vehicle {
  void moveForward(int meters);
}
```

*   **English:** `Vehicle` cannot be instantiated directly (e.g., `new Vehicle()` is error). It acts as a base for other classes like `Car`.
*   **Arabic:** (لا يمكن إنشاء نسخة مباشرة من `Vehicle`. هي تعمل كأساس لفئات أخرى مثل `Car`.)
*   **Analogy:** A "Building Plan" allows you to build specific houses, but you can't live in the plan itself.
    (تشبيه: "مخطط البناء" يسمح لك ببناء منازل محددة، لكن لا يمكنك العيش في المخطط نفسه.)

## `base`

**Concept:** Enforces inheritance.
(تفرض الوراثة.)

```dart
base class Vehicle {
  void moveForward(int meters) { ... }
}
```

*   **English:** Outside libraries can extend `Vehicle` but cannot implement it. This ensures the original implementation is always used.
*   **Arabic:** (يمكن للمكتبات الخارجية توسيع `Vehicle` ولكن لا يمكنها تنفيذها `implements`. هذا يضمن استخدام التنفيذ الأصلي دائمًا.)
*   **Analogy:** A "Family Recipe" – you can modify it for your own version (extend), but you can't just write a random recipe and call it the family recipe (implement).
    (تشبيه: "وصفة العائلة" - يمكنك تعديلها لإنشاء نسختك الخاصة، لكن لا يمكنك كتابة وصفة عشوائية وتسميتها وصفة العائلة.)

## `interface`

**Concept:** Enforces contract implementation.
(تفرض تنفيذ العقد.)

```dart
interface class Vehicle {
  void moveForward(int meters) { ... }
}
```

*   **English:** Outside libraries can implement `Vehicle` but cannot extend it. Good for defining API contracts where internal logic shouldn't be inherited.
*   **Arabic:** (يمكن للمكتبات الخارجية تنفيذ `Vehicle` ولكن لا يمكنها توسيعها. مفيدة لتحديد عقود API حيث لا ينبغي وراثة المنطق الداخلي.)
*   **Analogy:** A "Job Contract" – you agree to do the specific tasks (implement), but you don't inherit the boss's identity (extend).
    (تشبيه: "عقد العمل" - أنت توافق على القيام بمهام محددة، لكنك لا ترث هوية الرئيس.)

## `final`

**Concept:** Closes the hierarchy completely.
(تغلق التسلسل الهرمي تمامًا.)

```dart
final class Vehicle { ... }
```

*   **English:** Cannot be extended or implemented outside the library. It is completely locked down.
*   **Arabic:** (لا يمكن توسيعها أو تنفيذها خارج المكتبة. هي مغلقة تمامًا.)
*   **Analogy:** A "sealed envelope" or a "finished product" that cannot be modified or copied by others.
    (تشبيه: "ظرف مغلق" أو "منتج نهائي" لا يمكن تعديله أو نسخه من قبل الآخرين.)

## `sealed`

**Concept:** Enumerable set of subtypes.
(مجموعة معدودة من الأنواع الفرعية.)

```dart
sealed class Vehicle {}
class Car extends Vehicle {}
class Truck extends Vehicle {}
```

*   **English:** Useful for pattern matching. The compiler knows every possible subclass of `Vehicle`.
*   **Arabic:** (مفيدة لمطابقة الأنماط. المترجم يعرف كل فئة فرعية ممكنة لـ `Vehicle`.)
*   **Analogy:** A "Deck of Cards" – there are only specific types (Hearts, Clubs, etc.). You can't invent a new suit.
    (تشبيه: "أوراق اللعب" - هناك أنواع محددة فقط. لا يمكنك اختراع نوع جديد.)

## Key Takeaways

*   **`abstract`**: Cannot be instantiated.
*   **`base`**: Enforces inheritance (extends only).
*   **`interface`**: Enforces implementation (implements only).
*   **`final`**: No inheritance or implementation allowed outside.
*   **`sealed`**: Exhaustive subtypes (great for switch statements).
*   **Library Scope**: Most modifiers apply restrictions *outside* the defining library.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Modifier** | Keyword that changes the behavior of a declaration | مُعدّل | `abstract`, `final` |
| **Instantiate** | Creating a concrete object from a class | إنشاء مثيل | `var c = Car();` |
| **Extend** | Inheriting from a class (is-a relationship) | تمديد / وراثة | `class Car extends Vehicle` |
| **Implement** | Adhering to an interface contract | تنفيذ | `class Car implements Vehicle` |
| **Exhaustive** | Covering all possibilities | شامل / مستوفي | All `sealed` subtypes in a switch |
