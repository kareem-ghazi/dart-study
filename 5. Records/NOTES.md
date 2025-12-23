# Records

## Overview
**English:** Records in Dart are an anonymous, immutable, and aggregate type. They allow you to bundle multiple objects of different types into a single object. Unlike lists or maps, records have a fixed size and are strictly typed. They are useful for returning multiple values from functions or creating simple data structures without defining a class.

**Arabic:** (السجلات في Dart هي نوع بيانات مجهول الاسم، غير قابل للتغيير، ومجمّع. تتيح لك تجميع كائنات متعددة من أنواع مختلفة في كائن واحد. على عكس القوائم أو الخرائط، السجلات لها حجم ثابت وهي قوية النوع. إنها مفيدة لإرجاع قيم متعددة من الدوال أو إنشاء هياكل بيانات بسيطة دون الحاجة لتعريف فئة جديدة.)

---

## Record Syntax
**English:** Records are defined using comma-delimited lists enclosed in parentheses. They can contain both positional and named fields.
**Arabic:** (يتم تعريف السجلات باستخدام قوائم مفصولة بفاصلة ومحاطة بأقواس دائرية. يمكن أن تحتوي على حقول تعتمد على الموقع وحقول مسماة.)

```dart
// A record with positional and named fields
// (سجل يحتوي على حقول تعتمد على الموقع وحقول مسماة)
var record = ('first', a: 2, b: true, 'last');
```

**Analogy:**
*   **English:** Think of a record as a small, sealed package containing specific items. Some items are just thrown in (positional), while others have a label on them (named).
*   **Arabic:** (تخيل السجل كطرد صغير ومغلق يحتوي على عناصر محددة. بعض العناصر توضع كما هي (تعتمد على الموقع)، بينما البعض الآخر عليه ملصق باسمه (مسماة).)

---

## Record Fields and Access
**English:** You can access fields in a record using getters. Named fields are accessed by their name, while positional fields are accessed using the syntax `$1`, `$2`, etc.
**Arabic:** (يمكنك الوصول إلى الحقول في السجل باستخدام دوال "getters". يتم الوصول إلى الحقول المسماة باستخدام اسمها، بينما يتم الوصول إلى الحقول المعتمدة على الموقع باستخدام الصيغة `$1`, `$2`، وهكذا.)

```dart
var record = ('first', a: 2, b: true, 'last');

// Accessing positional fields
// (الوصول إلى الحقول المعتمدة على الموقع)
print(record.$1); // Prints 'first' (Skip named fields / يتخطى الحقول المسماة)
print(record.$2); // Prints 'last'

// Accessing named fields
// (الوصول إلى الحقول المسماة)
print(record.a); // Prints 2
```

---

## Record Types & Shape
**English:** Records are structurally typed. A record's "shape" depends on its fields, their types, and the names of the named fields. The order of named fields does not affect the shape, but the order of positional fields does.
**Arabic:** (السجلات تعتمد على البنية في تحديد نوعها. "شكل" السجل يعتمد على حقوله، وأنواعها، وأسماء الحقول المسماة. ترتيب الحقول المسماة لا يؤثر على الشكل، ولكن ترتيب الحقول المعتمدة على الموقع يؤثر.)

```dart
// These have different shapes (types) because field names differ
// (هذه السجلات لها أشكال مختلفة لأن أسماء الحقول مختلفة)
({int a, int b}) recordAB = (a: 1, b: 2);
({int x, int y}) recordXY = (x: 3, y: 4);

// Compile error! (خطأ برمجي!)
// recordAB = recordXY; 
```

---

## Record Equality
**English:** Two records are considered equal if they have the same shape and their fields have the same values.
**Arabic:** (يعتبر السجلان متساويين إذا كان لهما نفس الشكل وكانت حقولهما تحتوي على نفس القيم.)

```dart
(int x, int y, int z) point = (1, 2, 3);
(int r, int g, int b) color = (1, 2, 3);

// Positional fields match in type and order, so they are equal.
// (الحقول المعتمدة على الموقع تتطابق في النوع والترتيب، لذا فهي متساوية.)
print(point == color); // Prints 'true'
```

---

## Multiple Returns with Records
**English:** Records are the best way to return multiple values from a function cleanly and safely.
**Arabic:** (السجلات هي أفضل طريقة لإرجاع قيم متعددة من دالة بشكل نظيف وآمن.)

```dart
(String, int) getUserInfo(Map<String, dynamic> json) {
  return (json['name'], json['age']);
}

// Destructuring the returned record
// (تفكيك السجل المرجعي إلى متغيرات)
var (name, age) = getUserInfo({'name': 'Ali', 'age': 25});
print('User: $name, Age: $age');
```

---

## Important Notes & Warnings
*   **Immutability:** Records are immutable. Once created, their fields cannot be changed. (السجلات غير قابلة للتغيير. بمجرد إنشائها، لا يمكن تغيير حقولها.)
*   **Type Safety:** Records provide compile-time type checking, unlike `List` or `Map`. (توفر السجلات فحصًا للنوع وقت الترجمة، على عكس القوائم أو الخرائط.)
*   **Positional Access:** Positional fields start at `$1`, not `$0`. (الحقول المعتمدة على الموقع تبدأ من `$1` وليس `$0`.)

---

## Key Takeaways
*   Records bundle multiple values into a single object.
*   They can have positional and named fields.
*   Records are structurally typed based on their "shape".
*   They are ideal for multiple return values from functions.
*   Equality is based on shape and field values.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Record** | An anonymous, immutable, aggregate type. | سجل / قيد | `(1, 2)` |
| **Positional Field** | A field accessed by its position/order. | حقل يعتمد على الموقع | `record.$1` |
| **Named Field** | A field accessed by a specific name. | حقل مسمى | `record.age` |
| **Shape** | The structure definition (fields & types) of a record. | شكل / هيكل | `(int, String)` |
| **Immutable** | Cannot be changed after creation. | غير قابل للتغيير | `final`, `const` |
| **Destructuring** | Extracting values from a record into variables. | تفكيك / استخراج | `var (a, b) = record;` |
