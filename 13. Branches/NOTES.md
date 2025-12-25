# Branches

**Overview:**
Branching statements allow your code to take different paths depending on conditions. This is the decision-making logic of your program (e.g., "If it's sunny, wear a hat, else take an umbrella").

**(نظرة عامة):**
تسمح جمل التفرع للكود الخاص بك باتخاذ مسارات مختلفة اعتمادًا على شروط معينة. هذا هو منطق اتخاذ القرار في برنامجك (مثل: "إذا كان الجو مشمسًا، ارتدِ قبعة، وإلا خذ مظلة").

---

## 1. `if` and `else` (إذا و إلا)

The most basic way to check a condition.

```dart
if (age >= 18) {
  print('Adult');
} else if (age >= 13) {
  print('Teenager');
} else {
  print('Child');
}
```

---

## 2. `if-case` (إذا مع مطابقة النمط)

Checks if a value matches a specific pattern *and* extracts data if it does. This is cleaner than multiple `is` checks.

```dart
var pair = [10, 20];
if (pair case [int x, int y]) {
  print('Point: $x, $y');
}
```
*   **Analogy:** "If the box contains exactly two items, let me see them."
*   *(تشبيه: "إذا كان الصندوق يحتوي على عنصرين بالضبط، دعني أراهما".)*

---

## 3. `switch` Statement (جملة التبديل)

Used when you have many possible cases for a value. It executes statements (actions).

```dart
switch (command) {
  case 'OPEN':
    openDoor();
  case 'CLOSE':
    closeDoor();
  default:
    print('Unknown command');
}
```

---

## 4. `switch` Expression (تعبير التبديل)

Used when you want to **return a value** based on a match directly. It's more concise and functional.

```dart
var message = switch (statusCode) {
  200 => 'OK',
  404 => 'Not Found',
  _ => 'Error',
};
```
*   **Note:** Use `=>` instead of `:`.
*   *(ملاحظة: استخدم `=>` بدلاً من `:`.)*

---

## 5. Exhaustiveness Checking (التحقق من الشمولية)

Dart checks if you have covered **all possible cases**. This is especially powerful with `sealed` classes and `enums`.

*   **Sealed Class:** A class where all subtypes are known. Dart ensures your switch handles every subtype.
    *   *(فئة مختومة: فئة حيث تكون جميع أنواعها الفرعية معروفة. تضمن Dart أن جملة switch الخاصة بك تتعامل مع كل نوع فرعي.)*

---

## 6. Guard Clauses (`when`)

Add an extra condition to a case.

```dart
case [int a, int b] when a > b:
```
*   Matches a list of two integers ONLY if `a` is greater than `b`.

---

## Key Takeaways

*   Use `if` for simple boolean checks.
*   Use `switch` statements for complex logic or executing multiple lines of code per case.
*   Use `switch` expressions for assigning values cleanly.
*   **Guard clauses** (`when`) let you add logic to patterns.
*   **Sealed classes** give you safety by ensuring you never forget a case.

---

## Glossary (English-Arabic)

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Branching** | Splitting code execution into different paths. | تفرع | `if`, `switch` |
| **Case** | A specific scenario to match in a switch. | حالة | `case 'A':` |
| **Default** | The path taken if no other case matches. | افتراضي | `default:` |
| **Guard Clause** | A condition added to a pattern (`when`). | شرط حماية | `case x when x > 0` |
| **Exhaustive** | Covering all possible options. | شامل / مستوفي | Switching on all Enum values. |
