# Built-in Types

## Overview
Dart provides special support for several built-in types such as numbers, strings, and booleans. Since Dart is an object-oriented language, even these basic types are objects and can be initialized using literals or constructors.

(يوفر Dart دعمًا خاصًا للعديد من الأنواع المدمجة مثل الأرقام والنصوص والقيم المنطقية. نظرًا لأن Dart هي لغة موجهة للكائنات، فإن هذه الأنواع الأساسية تُعتبر كائنات ويمكن تهيئتها باستخدام القيم المباشرة أو المُنشئات.)

---

## Numbers

### Concept: `int` and `double`
Dart numbers are primarily of two types: `int` for integers (whole numbers) and `double` for floating-point numbers (numbers with decimals). Both inherit from the `num` type.

(`int` يستخدم للأعداد الصحيحة، و `double` يستخدم للأعداد العشرية. كلاهما يندرج تحت النوع `num`.)

### Code Example
```dart
var x = 1; // int
var y = 1.1; // double
num z = 1; // num can be int or double
z += 2.5;
```

### Explanation
*   **`var x = 1;`**: Defines an integer.
*   **`var y = 1.1;`**: Defines a double.
*   **`num z`**: A variable that can hold both `int` and `double` values.

(يُظهر الكود كيفية تعريف أعداد صحيحة وعشرية. المتغير من نوع `num` مرن ويمكنه تخزين كلا النوعين.)

### Analogy
Think of `int` as counting whole apples (1, 2, 3), and `double` as measuring water (1.5 liters, 0.25 liters).

(تخيل `int` مثل عد التفاحات الكاملة، و `double` مثل قياس الماء الذي قد يحتوي على كسور.)

---

## Strings

### Concept: String Creation and Interpolation
A `String` is a sequence of characters. You can use single or double quotes. Dart allows embedding variables directly inside strings using `$variable` or `${expression}`.

(النص `String` هو سلسلة من الأحرف. يمكنك استخدام علامات الاقتباس المفردة أو المزدوجة. يسمح Dart بدمج المتغيرات داخل النصوص باستخدام الرمز `$`.)

### Code Example
```dart
var s = 'world';
var message = 'Hello, $s!';
var shout = 'HELLO, ${s.toUpperCase()}!';
```

### Explanation
*   **`$s`**: Replaces `$s` with the value of variable `s`.
*   **`${s.toUpperCase()}`**: Evaluates the expression inside `{}` and inserts the result.

(`$s` يستبدل المتغير بقيمته. `${...}` يقوم بتنفيذ الكود داخل الأقواس ويدمج النتيجة في النص.)

### Analogy
String interpolation is like a "fill-in-the-blanks" form where Dart automatically fills in the information for you.

(دمج النصوص يشبه "ملء الفراغات" في استمارة، حيث يقوم Dart بملء المعلومات تلقائيًا.)

---

## Booleans

### Concept: `bool`
The `bool` type represents boolean values, which can only be `true` or `false`.

(النوع `bool` يمثل القيم المنطقية، والتي تكون إما `true` (صواب) أو `false` (خطأ).)

### Code Example
```dart
var isEmpty = true;
var hitPoints = 0;
assert(hitPoints == 0); // Checks if condition is true
```

### Explanation
*   **`true` / `false`**: The only two possible values.
*   **`assert(...)`**: Used to check if a boolean condition is true during development.

(القيم الوحيدة الممكنة هي `true` و `false`. تُستخدم `assert` للتأكد من صحة شرط معين أثناء التطوير.)

### Analogy
A `bool` is like a light switch: it is either ON (`true`) or OFF (`false`).

(الـ `bool` يشبه مفتاح الإضاءة: إما مشغل `true` أو مطفأ `false`.)

---

## Runes and Grapheme Clusters

### Concept: Unicode Support
Dart strings are sequences of UTF-16 code units. To handle special characters like emojis, we use Runes or the `characters` package.

(نصوص Dart هي تسلسل من وحدات UTF-16. للتعامل مع الرموز الخاصة مثل الإيموجي، نستخدم Runes أو حزمة `characters`.)

### Code Example
```dart
var heart = '\u2665'; // ♥
var emoji = '\u{1f606}'; // 😆
```

### Explanation
*   **`\uXXXX`**: Representation of a Unicode character.
*   **`\u{...}`**: Used for Unicode values with more than 4 digits (like emojis).

(تمثيل رموز يونيكود باستخدام `\u`. تُستخدم الأقواس `{}` للقيم الطويلة مثل الإيموجي.)

---

## Important Notes & Warnings

*   **Null Safety:** Remember that `int` cannot be null unless you declare it as `int?`. (تذكر أن المتغيرات لا تقبل قيمة `null` إلا إذا أضفت علامة الاستفهام `?` للنوع.)
*   **Int to Double:** An integer literal (like `1`) is automatically converted to `double` if the variable type is `double` (e.g., `double d = 1;` becomes `1.0`). (يتم تحويل الرقم الصحيح تلقائيًا إلى عشري إذا كان المتغير من نوع `double`.)
*   **String Constants:** Interpolation in `const` strings only works with other constants. (دمج النصوص في الثوابت `const` يعمل فقط مع ثوابت أخرى.)

## Key Takeaways

*   Dart has built-in support for `int`, `double`, `String`, `bool`, and more.
*   `num` is the parent type for both `int` and `double`.
*   Strings support interpolation using `$`.
*   Booleans are strictly `true` or `false`; 1 and 0 are not booleans.
*   Runes help display emojis and special symbols.
*   Symbols (`#name`) are mainly used for reflection/APIs.

## Glossary

| Term | Definition | Arabic Meaning | Example |
| :--- | :--- | :--- | :--- |
| **Literal** | A value written directly in the code (e.g., `5`, `'hello'`). | قيمة مباشرة | `var x = 5;` |
| **Interpolation** | Inserting values into a string using `$`. | دمج النصوص | `'Val: $x'` |
| **Rune** | A UTF-32 code point usually representing a character. | رمز يونيكود | `\u2665` |
| **Boolean** | A data type with two possible values: true or false. | منطقي | `bool isDone = false;` |
| **Bitwise** | Operations that manipulate individual bits of a number. | عمليات بتية | `<<`, `&`, `|` |
