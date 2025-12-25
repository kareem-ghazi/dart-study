# Patterns

**Overview:**
Patterns are a feature in Dart that allow you to test whether a value has a specific shape, type, or set of values, and then extract (destructure) data from it. They make code like data validation, object destruction, and switch cases much more concise and readable.

**(نظرة عامة):**
الأنماط (Patterns) هي ميزة في Dart تسمح لك باختبار ما إذا كانت القيمة ذات شكل أو نوع أو مجموعة قيم معينة، ومن ثم استخراج (تفكيك) البيانات منها. تجعل الأنماط كتابة الأكواد مثل التحقق من صحة البيانات، وتفكيك الكائنات، وحالات التبديل (switch cases) أكثر إيجازًا ووضوحًا.

---

## 1. Matching vs. Destructuring (المطابقة مقابل التفكيك)

Patterns perform two main tasks: **Matching** and **Destructuring**.

*   **Matching:** Checks if a value fits a certain criteria (like "Is this a list of two numbers?" or "Is this a String?").
    *   *(المطابقة: تتحقق مما إذا كانت القيمة تتناسب مع معايير معينة، مثل "هل هذه قائمة مكونة من رقمين؟" أو "هل هذا نص؟".)*
*   **Destructuring:** Extracts data from the matched value and assigns it to variables.
    *   *(التفكيك: يستخرج البيانات من القيمة المتطابقة ويسندها إلى متغيرات.)*

**Analogy:** Think of a **Shape Sorter** toy.
*   **Matching:** Checking if a block is a "Circle" shape.
*   **Destructuring:** Putting the block through the hole and collecting it in the box.

---

## 2. Places patterns can appear (أماكن استخدام الأنماط)

You can use patterns in various parts of your code.

### A. Variable Declaration (إعلان المتغيرات)

You can destructure values right when you declare variables.

```dart
// Declares new variables a, b, and c from the list and string.
var (a, [b, c]) = ('str', [1, 2]);
```
*   **Explanation:** This extracts `'str'` into `a`, `1` into `b`, and `2` into `c`.
*   *(شرح: هذا يستخرج "str" إلى a، و 1 إلى b، و 2 إلى c.)*

### B. Variable Assignment (إسناد المتغيرات)

Useful for **swapping variables** without a temporary variable.

```dart
var (a, b) = ('left', 'right');
(b, a) = (a, b); // Swap values directly
```
*   **Explanation:** The pattern `(b, a)` on the left receives the values from `(a, b)` on the right.
*   *(شرح: النمط (b, a) على اليسار يستقبل القيم من (a, b) على اليمين، مما يبدل القيم.)*

### C. Switch Statements & Expressions (جمل وتعبيرات Switch)

Patterns make `switch` very powerful. You can match values, ranges, and types.

```dart
switch (obj) {
  case 1: 
    print('One'); // Matches value 1
  case >= 10 && <= 20: 
    print('In range'); // Matches range
  case (var a, var b): 
    print('Record: $a, $b'); // Matches and destructures a record
}
```
*   **Explanation:** Each `case` tests the shape or value of `obj`.
*   *(شرح: كل حالة `case` تختبر شكل أو قيمة `obj`.)*

### D. Loops (الحلقات)

Destructure items directly in a `for` loop.

```dart
Map<String, int> scores = {'Alice': 10, 'Bob': 20};
for (var MapEntry(:key, :value) in scores.entries) {
  print('$key has $value points');
}
```
*   **Explanation:** Extracts `key` and `value` from each `MapEntry` in the map.
*   *(شرح: يستخرج المفتاح `key` والقيمة `value` من كل عنصر في الخريطة.)*

---

## 3. Use cases for patterns (حالات استخدام الأنماط)

### A. Destructuring Multiple Returns (تفكيك القيم المرجعة المتعددة)

When a function returns a Record (multiple values), patterns let you unpack them easily.

```dart
var (name, age) = getUserInfo(); 
// Instead of: var info = getUserInfo(); var name = info.$1; ...
```

### B. Validating JSON (التحقق من صحة JSON)

This is one of the most powerful uses. You can validate structure and types in one line.

```dart
var json = {'user': ['Ali', 25]};

// Single pattern validates: Map -> key 'user' -> List -> [String, int]
if (json case {'user': [String name, int age]}) {
  print('User $name is $age');
}
```
*   **Explanation:** If `json` matches the structure (Map with user list of String and int), it runs the code block with `name` and `age` variables ready to use.
*   *(شرح: إذا طابقت `json` الهيكل المحدد (خريطة تحتوي على قائمة مستخدم بها نص ورقم)، يتم تشغيل الكود مع جاهزية المتغيرات `name` و `age`.)*

---

## Key Takeaways

*   **Patterns** describe the shape of data.
*   **Matching** checks if data fits the shape.
*   **Destructuring** extracts data from the shape into variables.
*   **Wildcard (`_`)** can be used to ignore parts of a pattern.
*   **`if-case`** is a great way to "check and extract" in one step (especially for JSON).
*   **Refutable patterns** (like in `case`) might fail to match (and that's okay, execution continues).
*   **Irrefutable patterns** (like in `var` declaration) must always match or it's an error.

---

## Glossary (English-Arabic)

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Pattern** | A syntax to test data shape and extract values. | نمط | `case [a, b]:` |
| **Match** | Checking if a value fits a pattern. | مطابقة | `if (x case > 0)` |
| **Destructure** | Breaking a complex object into parts. | تفكيك / استخراج | `var (x, y) = point;` |
| **Refutable** | A pattern that can fail to match (e.g., in a switch case). | قابل للرفض (احتمال عدم المطابقة) | `case 1:` (fails if val is 2) |
| **Irrefutable** | A pattern that must always match (e.g., variable decl). | غير قابل للرفض (مطابقة حتمية) | `var (a, b) = (1, 2);` |
| **Guard Clause** | An extra condition (`when`) added to a pattern. | شرط حماية / شرط إضافي | `case var x when x > 5:` |
