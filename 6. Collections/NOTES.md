# Collections

## Overview
**English:** Dart provides robust built-in collection types: Lists (arrays), Sets (unique unordered items), and Maps (key-value pairs). It also supports advanced operators like spread (`...`) and control flow inside collections (`if`, `for`) to make building them dynamic and concise.
**Arabic:** (يوفر Dart أنواع تجميع بيانات قوية مدمجة: القوائم "Lists" (مصفوفات)، والمجموعات "Sets" (عناصر فريدة غير مرتبة)، والخرائط "Maps" (أزواج مفتاح-قيمة). كما يدعم عوامل تشغيل متقدمة مثل النشر (`...`) والتحكم في التدفق داخل المجموعات (`if`, `for`) لجعل بنائها ديناميكياً ومختصراً.)

---

## Lists (Arrays)
**English:** An ordered group of objects, accessible by index (starting at 0).
**Arabic:** (مجموعة مرتبة من الكائنات، يمكن الوصول إليها عن طريق الفهرس (يبدأ من 0).)

```dart
var list = [1, 2, 3];
print(list[0]); // 1
list.add(4);    // [1, 2, 3, 4]
```

**Analogy:**
*   **English:** A numbered to-do list where order matters.
*   **Arabic:** (قائمة مهام مرقمة حيث الترتيب مهم.)

---

## Sets
**English:** An unordered collection of unique items. Duplicate items are automatically ignored.
**Arabic:** (مجموعة غير مرتبة من العناصر الفريدة. يتم تجاهل العناصر المكررة تلقائياً.)

```dart
var halogens = {'fluorine', 'chlorine', 'fluorine'}; // 'fluorine' appears once
// (كلمة 'fluorine' تظهر مرة واحدة فقط)
```

**Analogy:**
*   **English:** A bag of unique marbles; having two identical marbles doesn't make sense in this context.
*   **Arabic:** (كيس من الكرات الزجاجية الفريدة؛ وجود كرتين متطابقتين ليس له معنى في هذا السياق.)

---

## Maps
**English:** A collection of key-value pairs. Keys must be unique, but values can be duplicated.
**Arabic:** (مجموعة من أزواج المفتاح-القيمة. يجب أن تكون المفاتيح فريدة، ولكن يمكن تكرار القيم.)

```dart
var gifts = {
  'first': 'partridge',
  'second': 'turtledoves'
};
print(gifts['first']); // partridge
```

**Analogy:**
*   **English:** A dictionary (word -> definition) or a phone book (name -> number).
*   **Arabic:** (قاموس (كلمة -> تعريف) أو دليل هاتف (اسم -> رقم).)

---

## Collection Operators & Control Flow
**English:** Dart allows you to use logic directly inside collection literals.
**Arabic:** (يسمح لك Dart باستخدام المنطق مباشرة داخل تعريف المجموعات.)

### Spread Operator (`...`)
**English:** Inserts all elements from another collection.
**Arabic:** (يدرج جميع العناصر من مجموعة أخرى.)

```dart
var list = [1, 2];
var list2 = [0, ...list, 3]; // [0, 1, 2, 3]
```

### Collection If
**English:** Conditionally adds an element.
**Arabic:** (يضيف عنصراً بشكل شرطي.)

```dart
var promoActive = true;
var nav = ['Home', 'Furniture', if (promoActive) 'Outlet'];
```

### Collection For
**English:** Builds a collection from another collection using a loop.
**Arabic:** (يبني مجموعة من مجموعة أخرى باستخدام حلقة تكرار.)

```dart
var listOfInts = [1, 2, 3];
var listOfStrings = [
  '#0',
  for (var i in listOfInts) '#$i'
]; // ['#0', '#1', '#2', '#3']
```

---

## Key Takeaways
*   **Lists** are ordered and indexed.
*   **Sets** contain unique items.
*   **Maps** store key-value associations.
*   Use `const` for unmodifiable collections.
*   Use `...` (spread) to merge collections.
*   Use `if` and `for` inside collections to build them dynamically.

---

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **List** | An ordered collection of items (array). | قائمة | `[1, 2, 3]` |
| **Set** | An unordered collection of unique items. | مجموعة | `{1, 2, 3}` |
| **Map** | A collection of key-value pairs. | خريطة (قاموس) | `{'a': 1, 'b': 2}` |
| **Spread Operator** | Inserts elements from one collection into another. | عامل النشر | `...list` |
| **Null-aware Spread** | Spreads a collection only if it's not null. | عامل النشر الآمن من Null | `...?list` |
| **Literal** | A notation for representing a fixed value in source code. | تعبير حرفي | `[]`, `{}` |
